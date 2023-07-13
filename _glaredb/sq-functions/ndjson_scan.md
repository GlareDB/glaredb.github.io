---
layout: default
title: ndjson_scan
parent: SQL functions
---

# `ndjson_scan`

Read a [newline delimeted JSON] file. The JSON file may exist locally or
remotely.

## Syntax

```sql
ndjson_scan(<url>)
```

| Field | Description                                                |
| ----- | ---------------------------------------------------------- |
| `url` | The URL or path to a [newline delimeted JSON] file to scan |

## Examples

In the following example, we start glaredb locally and query a log file in the
current working directory.

```console
$ touch log.json
$ echo '{"a":1}' > log.json
$ echo '{"b":2}' >> log.json
./glaredb local
GlareDB (v0.2.0)
Type \help for help.
Using in-memory catalog
〉select * from ndjson_scan('./log.json');
+------+------+
| a    | b    |
+------+------+
| 1    | NULL |
| NULL | 2    |
+------+------+
〉
```

[newline delimeted JSON]: https://github.com/ndjson/ndjson-spec
