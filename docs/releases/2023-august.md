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

## SQL workspace improvements

**Available in**: [GlareDB Cloud]

- Tutorials were added to demonstrate connecting and reading external sources.
  The tutorials can be accessed by clicking the info icon on the top right of
  the results panel. To switch back to results view, click the table icon.

  ![tutorials]
  ![tutorial-toggle]

- Double-clicking a table in the explorer generates a `SELECT` query
- The explorer added Views and distinguishes external from default databases
- The results view was redesigned. In a multi-query statement, all results are
  now shown as tabs, even if one of the statements returned nothing.

## Native tables: UPDATE, DELETE and CREATE AS

**Available in**: [GlareDB@v0.3.0], [GlareDB Cloud]

A table can be created from a query:

```sql
CREATE TABLE t1 AS SELECT * FROM generate_series(1, 5, 2);
```

**Available in**: [GlareDB@v0.4.0], [GlareDB Cloud]

Native tables now support UPDATE and [`DELETE`] statements:

```sql
CREATE TABLE public.users ( name text );
INSERT INTO public.users VALUES ('Eldon');
UPDATE public.users SET name = 'Eldon Tyrell' WHERE name = 'Eldon';
DELETE FROM public.users;
```

## Improvements to SQL functions

**Available in**: [GlareDB@v0.3.0], [GlareDB Cloud]

- You can now glob (`**` and `*`) to scan multiple files and directories. See
  [`csv_scan`], for example.
- `delta_scan` function was added to query delta tables from local paths, s3
  and gcs
- All `*_scan` functions received support for passing multiple URLs

**Available in**: [GlareDB@v0.4.0], [GlareDB Cloud]

- [`generate_series`] now supports decimals

## Exclude columns in SELECT

**Available in**: [GlareDB@v0.3.0], [GlareDB Cloud]

[`SELECT`] now accepts an [`EXCLUDE`] clause to exclude specific columns
from output:

```sql
SELECT * EXCLUDE (id) FROM users;
```

## Misc updates and fixes

**Available in**: [GlareDB@v0.3.0], [GlareDB Cloud]

- Fixed `CREATE SCHEMA IF NOT EXISTS` failing if schema existed

**Available in**: [GlareDB@v0.3.0]

- [`glaredb local`] now has prettier output
- [Python bindings] now include `show()` with pretty formatting and `close()`
  for gracefully closing connections.

**Available in**: [GlareDB Cloud]

- Fixed an issue where the button for adding an SSH tunnel was not displaying
- Organization billing now contains historic billing data
- The sign in page was redesigned
- The SQL workspace is now the first page users are loaded into when they sign
  in

[GlareDB@v0.4.0]: https://github.com/GlareDB/glaredb/releases/tag/v0.4.0
[GlareDB@v0.3.0]: https://github.com/GlareDB/glaredb/releases/tag/v0.3.0
[GlareDB Cloud]: https://console.glaredb.com/
[tutorials]: /assets/images/tutorials.png
[tutorial-toggle]: /assets/images/tutorial-toggle.png
[`DELETE`]: /glaredb/sql-commands/delete/
[`csv_scan`]: /glaredb/sq-functions/csv_scan/
[`generate_series`]: /glaredb/sq-functions/generate_series/
[`SELECT`]: /glaredb/sql-commands/select/
[`EXCLUDE`]: /glaredb/sql-commands/select/#exclude-clause
[`glaredb local`]: /glaredb/local/
[Python bindings]: /glaredb/python/
