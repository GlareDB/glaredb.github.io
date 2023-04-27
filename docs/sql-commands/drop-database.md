---
layout: default
title: DROP DATABASE
parent: SQL commands
---

<!-- markdownlint-disable title-case-style -->

# DROP DATABASE

<!-- markdownlint-enable title-case-style -->

Drop a database. The `default` database cannot be dropped.

Note that this does not make any modifications to the external data source, and
only means the database can no longer be accessed from within GlareDB.

## Syntax

```sql
DROP DATABASE [IF EXISTS] <database>;
```

| Field      | Description           |
|------------|-----------------------|
| `database` | The database to drop. |

## Examples

Drop a database named `pg`. See [CREATE EXTERNAL DATABASE] for adding a database.

```sql
DROP DATABASE pg;
```

[CREATE EXTERNAL DATABASE]: {{site.baseurl}}/docs/sql-commands/create-external-database
