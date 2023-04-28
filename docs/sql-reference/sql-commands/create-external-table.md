---
layout: default
title: CREATE EXTERNAL TABLE
parent: SQL commands
grand_parent: SQL reference
---

<!-- markdownlint-disable title-case-style -->

# CREATE EXTERNAL TABLE

<!-- markdownlint-enable title-case-style -->

Create an external table backed by a data source.

## Syntax

```sql
CREATE EXTERNAL TABLE [IF NOT EXISTS] <table-name>
    FROM <data-source-type>
    OPTIONS (<data-source-options>);
```

| Field                 | Description                                      |
| --------------------- | ------------------------------------------------ |
| `table-name`          | Name of the database as it appears in GlareDB.   |
| `data-source-type`    | The type of data source, for example `postgres`. |
| `data-source-options` | Options specific to this data source type.       |

`table-name` may optionally be qualified with a schema.

Specifying `IF NOT EXISTS` will suppress an error if `schema-name` already
exists.

## Examples

Create an external table named `external_table` using a Postgres data source.
The external table will be backed by the `users` table in the `public` schema on
the remote Postgres instance.

```sql
CREATE EXTERNAL TABLE external_table
    FROM postgres
    OPTIONS (
        host = 'my.postgres.host',
        port = '5432',
        user = 'glaredb',
        password = 'password',
        database = 'glaredb_test',
        schema = 'public',
        table = 'users'
    );
```
