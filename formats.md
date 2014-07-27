## Background

Nightscout has two formats in use today.

Let's give them names:

#### `BeeGee` existing http schema
Looks like this:
[code](https://github.com/jasoncalabrese/project-glu/blob/master/lib/models/entry.js#L12-L17)

```javascript
{
  _id: String,
  timestamp: Date,
  bg: Number,
  direction: String
}
```

#### `Sandstone` existing mongo upload
This is what the
[`uploader`](https://gist.github.com/bewest/e0ff794726f122723282#currently-used)
sends directly to mongo.

```javascript
{
  dateString: <some non 8601 RFC>
, date: <some local epoch>
, sgv: <alias of bg>
, direction: <string>
, device: <optional string>  

}

```
## Problems
Both formats have problems.
There is a general consensus to converge on transmitting 8601 timestamps with timezone attached.

Following proposals to get around some of these probblems:
* use `timestamp` as the sole field, it **MUST** be 8601
  * timezone **SHOULD** be attached, if absent Zulu/UTC will be assumed.
* records should have hash to help dedupe
 * records should identify their schema and type, let's stuff all three in a field called `_sig` for "signature."

#### `Practical8601`
```javascript
{
  timestamp: "<ISO8601 format with [any] timezone>"
  epoch: <optional, mostly ignored UTC epoch>
  sgv: <alias of bg>
  direction: <string or enum>
  device: <string or enum>

}

```

#### `SigIntro`
```javascript
{
  timestamp: "<ISO8601 format on Zulu time>"
  sgv: <alias of bg>
  direction: <string or enum>
  device: <string or enum>
  _sig: "sgv://$schema/$hash"
}

```

### sgvdata
Sgvdata should implement several migrations, perhaps using https://github.com/visionmedia/node-migrate and filters to transition between these formats.

##### `sgvdata.sync.beegee` -> `sandstone`

For renaming of fields.

* If `bg` field, rename to `sgv`
* If `timestamp` field, rename to `dateString`
* Create `date`

##### `sgvdata.sync.sandstone` -> `Practical8601`

To standardize on 8601.
* If `date` and `dateString` are present
  * if `dateString` is 8601, delete `date` rename to `timestamp`
  * if `no `dateString`, use `date` epoch, convert to 8601, save in `timestamp`, delete `date`

Then filter records so reformat 8601 so that it is in zulu time.

#### `sgvdata.sync.Practical8601` -> `SigIntro`

* parse `dateString` as 8601, re-emit in 8601 in zulu time as `timestamp`.
* create new `_sig` field, used to capture type of document, schema used, and hash of values in uri syntax:
  * let `$hash` equal sha1sum of `timestamp, sgv, direction`
  * let `$type` equal `sgv`
  * let `$schema` equal `SigIntro`
  * eg, `sgv://SigIntro/ab4d3adb33f`

Each of these can be can be used to configure an up/down type of filter stream, eg:

```javascript
// stream to convert any `BeeGee` entries via mongo schema to schema'd entries
var BeeGee2SigIntro = es.pipeline(
  sgvdata.writable(sgvdata.sync.BeeGee)
, sgvdata.writable(sgvdata.sync.SandStone)
, sgvdata.writable(sgvdata.sync.PracticalISO8601)
, sgvdata.writable(sgvdata.sync.SigIntro)
;

```

Other streams to/from could be easily configured.