---
layout: default
title: list_schemas
parent: SQL functions
grand_parent: Reference
---

# `list_schemas`

List schemas for a database.

The database must be in scope of GlareDB, for example as a data source.

## Syntax

```sql
list_schemas(<database>)
```

| Field      | Description                                   |
| ---------- | --------------------------------------------- |
| `database` | The name of the database to list schemas for. |

## Examples

In the following example, suppose a Postgres data source was added to GlareDB
and named `my_pg`:

```sql
select * from list_schemas(my_pg);
```

See [CREATE EXTERNAL DATABASE] for adding a database as a data source.

[CREATE EXTERNAL DATABASE]: /reference/sql-commands/create-external-database/
