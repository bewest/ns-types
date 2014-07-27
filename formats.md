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


#### V1 `Practical8601`
```javascript
{
  timestamp: "<ISO8601 format with [any] timezone>"
  epoch: <optional, mostly ignored UTC epoch>
  sgv: <alias of bg>
  direction: <string or enum>
  device: <string or enum>

}

```
