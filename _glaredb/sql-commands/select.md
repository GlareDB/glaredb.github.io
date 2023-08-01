---
layout: default
title: SELECT
parent: SQL commands
---

# SELECT

The SQL standard for `SELECT` is large and powerful so that you can query data
with very precise parameters. GlareDB supports most of the [PostgreSQL `SELECT`]
syntax and will eventually have full support.

## Syntax

```sql
SELECT [ DISTINCT ]
    [ * [ EXCLUDE ( column [, ...] ) ] | expression [ [ AS ] output_name ] [, ...] ]
    [ FROM from_item [, ...] ]
    [ WHERE condition ]
    [ GROUP BY [ DISTINCT ] grouping_element [, ...] ]
    [ HAVING condition ]
    [ { UNION | INTERSECT | EXCEPT } [ ALL | DISTINCT ] select ]
    [ ORDER BY expression [ ASC | DESC | USING operator ] [ NULLS { FIRST | LAST } ] [, ...] ]
    [ LIMIT { count | ALL } ]
    [ OFFSET start [ ROW | ROWS ] ]
```

| Field              | Description                                   |
| ------------------ | --------------------------------------------- |
| `expression`       | An SQL expression                             |
| `output_name`      | An alias (alternative name)                   |
| `from_item`        | Source table to select from                   |
| `condition`        | An SQL expression that evaluates to a boolean |
| `grouping_element` | Column to group on                            |
| `operator`         | `UNION`, `INTERSECT` or `EXCEPT` operator     |
| `count`            | Number (ex: of rows to limit)                 |
| `start`            | Number (ex: of rows to offset)                |

## Examples

There are _many_ formats of select queries. In the following example a data
source named `pg` with a `public` schema and `users` table is queryed. The query
looks for all names starting with `G` and returns a count of duplicates.

```sql
select name, count(id) as count
  from pg.public.users
  group by name
  having name like 'G%'
  order by name asc;
```

```text
       name       | count
------------------+-------
 Gary             |     1
 Gloria           |     2
(2 rows)

```

### Exclude clause

The `EXCLUDE` clause will select all columns except those specified.

```sql
-- select all columns except id
SELECT * EXCLUDE (id) FROM pg.public.users;
```

[PostgreSQL `SELECT`]: https://www.postgresql.org/docs/current/sql-select.html
