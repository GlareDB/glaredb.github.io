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
-- creating a table from a SELECT with aliasing and casting
CREATE TABLE table_name (column_name data_type [, ...]) AS select_statement;
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
CREATE TABLE public.ints AS select * from generate_series(1, 10);
```

In these examples, we leverage casting and aliasing when creating a table and
values from a [`SELECT`]. Note that not all columns need to be aliased. The
provided values will be casted to match the column data type.

```sql
-- The first column will be aliased to 'a' and cast to Int32. The second column
-- will be unnamed at Int64.
CREATE TABLE public.example (a int) AS VALUES (1, 2);

-- Both columns are aliased and cast from values. The first column will be 'a'
-- and the value 1 is cast to Int32. The second column will be 'b' and the value
-- 2 is cast to Utf8 text.
CREATE TABLE public.example2 (a int, b text) as values (1, 2);
```

[`SELECT`]: /glaredb/sql-commands/select/
[`generate_series`]: /glaredb/sq-functions/generate_series/
