---
layout: default
title: csv_scan
parent: SQL functions
---

# `csv_scan`

Read a CSV file. The CSV file may exist locally or remotely.

## Syntax

```sql
csv_scan(<url>)
```

| Field | Description                           |
| ----- | ------------------------------------- |
| `url` | The URL or path to a CSV file to scan |

Note that `new-name` must be unique within a GlareDB deployment.

## Examples

The following example selects 10 rows from a CSV hosted in a public GlareDB
demo bucket.

```sql
select * from csv_scan (
  'https://storage.googleapis.com/glaredb-demos/tyrell/voight_kampff.csv'
)
limit 10;
```

In the next example, we start glaredb locally and query a CSV file in the
current working directory.

```console
$ touch test.csv
$ echo "a,b,c" > test.csv
$ echo "1,2,3" >> test.csv
./glaredb local
GlareDB (v0.2.0)
Type \help for help.
Using in-memory catalog
〉select * from csv_scan('./test.csv');
+---+---+---+
| a | b | c |
+---+---+---+
| 1 | 2 | 3 |
+---+---+---+
〉
```
