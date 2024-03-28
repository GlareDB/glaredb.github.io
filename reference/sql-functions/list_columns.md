---
layout: default
title: list_columns
parent: SQL functions
grand_parent: Reference
---

# `list_columns`

List columns for a table.

The database that the tables belong to must be in scope of GlareDB, for example
as a data source.

For listing columns on a native table, use `"default"` as the database.

## Syntax

```sql
list_columns(<database>, <schema>, <table>)
```

| Field      | Description                                |
| ---------- | ------------------------------------------ |
| `database` | The name of the database.                  |
| `schema`   | The name of the schema on the databsae.    |
| `table`    | The name of the table to list columns for. |

## Examples

In the following example, suppose a Postgres data source was added to GlareDB
and named `my_pg`:

```sql
-- list all columns of the public.customers table
select * from list_columns("my_pg", "public", "customers");
```

See [CREATE EXTERNAL DATABASE] for adding a database as a data source.

[CREATE EXTERNAL DATABASE]: /glaredb/sql-commands/create-external-database/
