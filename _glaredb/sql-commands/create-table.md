---
layout: default
title: CREATE TABLE
parent: SQL commands
---

# CREATE TABLE

Create a native table.

{: .important}

> GlareDB does not yet support UPDATE for native tables.

## Syntax

```sql
-- defining a table, optionally with VALUES
CREATE TABLE table_name (column_name data_type [, ... ])
[AS VALUES (value)[, ... ]];
-- creating a table from a SELECT
CREATE TABLE table_name AS select_statement;
```

| Field              | Description                                       |
| ------------------ | ------------------------------------------------- |
| `column_name`      | Name of a column.                                 |
| `data_type`        | Data type of a column.                            |
| `select_statement` | A [`SELECT`] query to create the table from.      |
| `table_name`       | Name of the table.                                |
| `value`            | A value set to insert into the table on creation. |

## Examples

In this example a simple users table is created with two users:

```sql
CREATE TABLE public.users ( name text, email text ) AS VALUES
  ('Pris', 'pris@stratton.net'),
  ('Eldon Tyrell', 'ceo@tyrell.corp');
```

In this example, we create a table schema and values from [`generate_series`].

```sql
CREATE TABLE AS select * from generate_series(1, 10);
```

[`SELECT`]: /glaredb/sql-commands/select/
[`generate_series`]: /glaredb/sq-functions/generate_series/
