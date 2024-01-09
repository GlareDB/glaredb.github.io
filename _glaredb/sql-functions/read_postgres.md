---
layout: default
title: read_postgres
parent: SQL functions
---

# `read_postgres`

Read a Postgres table. The table does not have to be a known data source to
GlareDB.

## Syntax

```sql
read_postgres(<connection_str>, <schema>, <table>)
```

| Field            | Description                                     |
| ---------------- | ----------------------------------------------- |
| `connection_str` | A Postgres connection string.                   |
| `schema`         | The name of the schema where the table resides. |
| `table`          | The name of the table to query.                 |

## Examples

In the following example, a 'users' table located in a Postgres database is
queryed.

```sql
select * from read_postgres(
  'host=your.host port=5432 user=postgres password=postgres database=postgres',
  'public',
  'users'
);
```

Refer to the [documentation on Postgres data sources] for more information.

[documentation on Postgres data sources]: /docs/data-sources/supported/postgres
