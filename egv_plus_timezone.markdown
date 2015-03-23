
## sgv

```bash
cat sgv.json | wc 
      1      11     130

```

Proposal:
Binary to save bytes:

Original EGV:
https://github.com/compbrain/dexcom_reader/blob/master/database_records.py#L149-L153
```
  # uint, uint, ushort, byte, ushort
  # (system_seconds, display_seconds, glucose, trend_arrow, crc)
  FORMAT = '<2IHcH'

```

But we also need either system time or delta from system time to get timezone offset.
