---
layout: default
title: list_tables
parent: SQL functions
grand_parent: Reference
---

# `list_tables`

List tables for a schema.

The database where the schema resides must be in scope of GlareDB, for example
as a data source.

## Syntax

```sql
list_tables(<database>, <schema>)
```

| Field      | Description                                |
| ---------- | ------------------------------------------ |
| `database` | The name of the database.                  |
| `schema`   | The name of the schema to list tables for. |

## Examples

In the following example, suppose a Postgres data source was added to GlareDB
and named `my_pg` and has a `public` schema:

```sql
select * from list_tables(my_pg, public);
```

See [CREATE EXTERNAL DATABASE] for adding a database as a data source.

[CREATE EXTERNAL DATABASE]: /reference/sql-commands/create-external-database/
