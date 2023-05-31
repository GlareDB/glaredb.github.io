---
layout: default
title: ALTER DATABASE
parent: SQL commands
grand_parent: SQL reference
---

# ALTER DATABASE

Alter a database. The `default` database cannot be dropped.

GlareDB currently only supports renaming a database using this command.

## Syntax

```sql
ALTER DATABASE <database-name> RENAME TO <new-name>;
```

| Field           | Description                     |
| --------------- | ------------------------------- |
| `database-name` | Name of the database to rename. |
| `new-name`      | New name for the database.      |

Note that `new-name` must be unique within a GlareDB deployment.

## Examples

Rename database `db1` to `db2`. See [CREATE EXTERNAL DATABASE] for adding a database.

```sql
ALTER DATABASE db1 RENAME TO db2;
```

[CREATE EXTERNAL DATABASE]: /docs/sql-reference/sql-commands/create-external-database.html
