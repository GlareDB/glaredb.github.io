---
layout: default
title: UPDATE
parent: SQL commands
---

# UPDATE

The SQL standard for `UPDATE` is large and powerful
so that you can update rows from a table with precise
control. GlareDB supports most of the [PostgreSQL `UPDATE`]
syntax and will eventually have full support.

## Syntax

```sql
UPDATE table_name
    SET column = value_expr [, ...]
    [ WHERE condition ]
```

| Field        | Description                                                 |
| ------------ | ----------------------------------------------------------- |
| `table_name` | The fully-qualified table name to update (ex: public.users) |
| `column`     | A column to update. Column is not qualified (ex: name)      |
| `value_expr` | An SQL expression that evaluates to the column value        |
| `condition`  | An SQL expression that evaluates to a boolean               |

## Examples

Update all rows from table `table1` and set value of col1 to 3.

```sql
UPDATE table1
  SET col1 = 3;
```

Update rows from table `table2` and set columns `col1` and `col2` to
2 and 4 respectively, where column `col2` has value 3.

```sql
UPDATE table2
  SET col1 = 2, col2 = 4
  WHERE col2 = 3;
```

[PostgreSQL `UPDATE`]: https://www.postgresql.org/docs/current/sql-update.html
