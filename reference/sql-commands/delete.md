---
layout: default
title: DELETE
parent: SQL commands
grand_parent: Reference
---

# DELETE

The SQL standard for `DELETE` is large and powerful
so that you can delete rows from a table with precise
control. GlareDB supports most of the [PostgreSQL `DELETE`]
syntax and will eventually have full support.

## Syntax

```sql
DELETE FROM table_name
    [ WHERE condition ]
```

| Field        | Description                                   |
| ------------ | --------------------------------------------- |
| `table_name` | Source table to delete from                   |
| `condition`  | An SQL expression that evaluates to a boolean |

## Examples

Delete all rows from table `table1`.

```sql
DELETE FROM table1;
```

Delete rows from table `table2` where column `col_int` has a value greater than 10.

```sql
DELETE FROM table2
  WHERE col_int > 10;
```

[PostgreSQL `DELETE`]: https://www.postgresql.org/docs/current/sql-delete.html
