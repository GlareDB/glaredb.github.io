---
layout: default
title: read_postgres
parent: SQL functions
grand_parent: Reference
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

In the following example, a 'customer' table located in a Postgres database is
queryed. Try it out!

```sql
SELECT * FROM read_postgres(
  'host=pg.demo.glaredb.com port=5432 user=demo password=demo dbname=postgres',
  'public',
  'customer'
);
```

The same table can be queried using the `postgresql://` connection string
format:

```sql
SELECT * FROM read_postgres(
  'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres',
  'public',
  'customer'
);
```

Refer to the [documentation on Postgres data sources] for more information.

[documentation on Postgres data sources]: /data-sources/postgres
