---
layout: default
title: read_sqlserver
parent: SQL functions
grand_parent: Reference
---

# `read_sqlserver`

Read a SQL Server table. The table does not have to be a known data source to
GlareDB.

## Syntax

```sql
read_sqlserver(<connection_string>, <schema>, <table>)
```

| Field               | Description                                  |
| ------------------- | -------------------------------------------- |
| `connection_string` | A SQL Server connection string.              |
| `schema`            | The name of the schema containing the table. |
| `table`             | The name of the table to query.              |

## Examples

In the following example, a 'users' table located in a SQL Server database is
queryed.

```sql
select * from read_sqlserver(
  'server=tcp:my.sqlserver.host,1433;user=SA;password=Password123;TrustServerCertificate=true',
  'dbo',
  'users'
);
```

Refer to the [documentation on SQL Server data sources] for more information.

[documentation on SQL Server data sources]: /docs/data-sources/supported/sql-server
