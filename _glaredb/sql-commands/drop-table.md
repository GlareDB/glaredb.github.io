---
layout: default
title: DROP TABLE
parent: SQL commands
---

# DROP TABLE

Drop a table. Note that builtin system tables cannot be dropped. See [system
catalog] for an overview of builtin tables and views.

## Syntax

```sql
DROP TABLE [IF EXISTS] <table-name>;
```

| Field        | Description        |
| ------------ | ------------------ |
| `table-name` | The table to drop. |

`table-name` may optionally be qualified with a schema name.

## Examples

Drop a table named `my_table`. See [CREATE EXTERNAL TABLE] for how to create an
external table.

```sql
DROP TABLE my_table;
```

[CREATE EXTERNAL TABLE]: /glaredb/sql-commands/create-external-table.html
[system catalog]: /glaredb/system-catalog/
