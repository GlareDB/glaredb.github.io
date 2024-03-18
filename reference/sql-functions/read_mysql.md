---
layout: default
title: read_mysql
parent: SQL functions
grand_parent: Reference
---

# `read_mysql`

Read a MySQL table. The table does not have to be a known data source to
GlareDB.

## Syntax

```sql
read_mysql(<connection_str>, <schema>, <table>)
```

| Field            | Description                                     |
| ---------------- | ----------------------------------------------- |
| `connection_str` | A MySQL connection string.                      |
| `schema`         | The name of the schema where the table resides. |
| `table`          | The name of the table to query.                 |

## Examples

In the following example, a 'users' table located in a MySQL database is
queryed.

```sql
select * from read_mysql(
  'host=your.host port=3306 user=mysql password=password database=database',
  'public',
  'users'
);
```

Refer to the [documentation on MySQL data sources] for more information.

[documentation on MySQL data sources]: /docs/data-sources/supported/mysql
