---
layout: default
title: parquet_scan
parent: SQL functions
---

# `parquet_scan`

Read a parquet file. The file may exist locally or remotely.

## Syntax

```sql
parquet_scan(<url>)
```

| Field | Description                              |
| ----- | ---------------------------------------- |
| `url` | The URL or path to a parqet file to scan |

## Examples

In the following example we start glaredb locally, use [COPY TO] to create a
parquet file and finally read it with `parquet_scan`.

```console
$ ./glaredb local
GlareDB (v0.2.0)
Type \help for help.
Using in-memory catalog
〉copy (select 1) to local format parquet (location 'example.parquet');
copy success
〉select * from parquet_scan('./example.parquet');
+----------+
| Int64(1) |
+----------+
| 1        |
+----------+
〉
```

[COPY TO]: /glaredb/sql-commands/copy-to
