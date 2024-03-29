---
layout: default
title: ALTER DATABASE
parent: SQL commands
grand_parent: Reference
---

# ALTER DATABASE

Alter a database. The `default` database cannot be dropped.

With this command, GlareDB supports:

- renaming a database
- setting the access mode of an external database

## Syntax

```sql
ALTER DATABASE <database-name>
  [RENAME TO <new-name>]
  [SET ACCESS_MODE TO <access-mode>];
```

| Field           | Description                           |
| --------------- | ------------------------------------- |
| `database-name` | Name of the database to rename.       |
| `new-name`      | New name for the database.            |
| `access-mode`   | One of: \[`READ_WRITE`, `READ_ONLY`\] |

Note that `new-name` must be unique within a GlareDB deployment.

## Examples

Rename database `db1` to `db2`. See [CREATE EXTERNAL DATABASE] for adding a
database.

```sql
ALTER DATABASE db1 RENAME TO db2;
```

Create a Postgres data source and set it to `READ_ONLY`:

```sql
CREATE EXTERNAL DATABASE my_pg
    FROM postgres
    OPTIONS (
        host = 'my.postgres.host',
        port = '5432',
        user = 'glaredb',
        password = 'password',
        database = 'glaredb_test',
    );

ALTER DATABASE my_pg SET ACCESS_MODE TO READ_ONLY;
```

[CREATE EXTERNAL DATABASE]: /reference/sql-commands/create-external-database/
