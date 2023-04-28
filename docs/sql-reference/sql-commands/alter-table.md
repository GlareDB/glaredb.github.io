---
layout: default
title: ALTER TABLE
parent: SQL commands
grand_parent: SQL reference
---

<!-- markdownlint-disable title-case-style -->

# ALTER TABLE

<!-- markdownlint-enable title-case-style -->

Alter a table. Note that builtin system tables cannot be altered. See [system
catalog] for an overview of builtin tables and views.

GlareDB currently only supports renaming a table using this command.

## Syntax

```sql
ALTER TABLE <table-name> RENAME TO <new-name>;
```

| Field        | Description                  |
| ------------ | ---------------------------- |
| `table-name` | Name of the table to rename. |
| `new-name`   | New name for the table.      |

`table-name` may optionally be qualified with a schema.

## Examples

Rename table `t1` to `t2`. See [CREATE EXTERNAL TABLE] for adding a table.

```sql
ALTER TABLE t1 RENAME TO t2;
```

[CREATE EXTERNAL TABLE]: {{site.baseurl}}/docs/sql-commands/create-external-table
[system catalog]: {{site.baseurl}}/docs/system-catalog
