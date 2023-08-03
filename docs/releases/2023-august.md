---
layout: default
title: August 2023
parent: "Release notes"
---

# August 2023

## Initial Iceberg support

**Available in**: [GlareDB@v0.3.0], [GlareDB Cloud]

We've added _initial_ support for reading Iceberg tables with `iceberg_scan`,
`iceberg_snapshots` and `iceberg_data_files` SQL functions. See
<https://github.com/GlareDB/glaredb/issues/1448> for more details on what's to
come in future releases.

## Create native table from query

**Available in**: [GlareDB@v0.3.0], [GlareDB Cloud]

A table can be created from a query:

```sql
create table t1 as select * from generate_series(1, 5, 2);
```

## Improvements to SQL functions

**Available in**: [GlareDB@v0.3.0], [GlareDB Cloud]

- You can now glob (`**` and `*`) to scan multiple files and directories. See
  [`csv_scan`], for example.
- `delta_scan` function was added to query delta tables from local paths, s3
  and gcs
- All `*_scan` functions received support for passing multiple URLs

## Exclude columns in SELECT

**Available in**: [GlareDB@v0.3.0], [GlareDB Cloud]

[`SELECT`] now accepts an `EXCEPT` or `EXCLUDE` clause to exclude specific columns
from output:

```sql
SELECT * EXCLUDE (id) FROM users;
```

## Misc updates and fixes

**Available in**: [GlareDB@v0.3.0], [GlareDB Cloud]:

- Fixed `CREATE SCHEMA IF NOT EXISTS` failing if schema existed

**Available in**: [GlareDB@v0.3.0]:

- [`glaredb local`] now has prettier output
- [Python bindings] now include `show()` with pretty formatting and `close()`
  for gracefully closing connections.

[GlareDB@v0.3.0]: https://github.com/GlareDB/glaredb/releases/tag/v0.3.0
[GlareDB Cloud]: https://console.glaredb.com/
[`csv_scan`]: /glaredb/sq-functions/csv_scan/
[`SELECT`]: /glaredb/sql-commands/select/
[`glaredb local`]: /glaredb/local/
[Python bindings]: /glaredb/python/
