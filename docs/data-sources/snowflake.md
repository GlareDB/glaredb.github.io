---
layout: default
title: Snowflake
parent: Data sources
---

# Snowflake

Snowflake is able to be used as an external data source. Either an entire
database or a single table may be added as a data source.

## External database

An entire Snowflake database can be added using the [CREATE EXTERNAL DATABASE]
command.

{: .important}

> There are two equivalent formats. In both formats, `database-name` will be the
> name of the database inside GlareDB. This cannot be qualified, and must be
> unique across all other databases in the deployment.


```sql
CREATE EXTERNAL DATABASE <database-name>
  FROM snowflake
  OPTIONS (
    account_name = '<account-name>',
    login_name = '<login-name>',
    password = '<password>',
    database_name = '<database_name>',
    warehouse = '<warehouse>',
    role_name = '<role-name>',
  );
```

### External database long format options

| Field           | Description                                               |
|-----------------|-----------------------------------------------------------|
| `account-name`  | Account containing the Snowflake warehouse to connect to. |
| `login-name`    | Name of the user to login as.                             |
| `password`      | Password for the above user.                              |
| `database-name` | Name of the database to connect to.                       |
| `warehouse`     | Name of the warehouse to connect to.                      |
| `role-name`     | Role to use when connecting.                              |

## External table

Adding an external table can be done through the [CREATE EXTERNAL TABLE]
command.

{: .important}

> There are two equivalent foramts. In both formats, `table-name` will be the
> name of the database inside GlareDB. `table-name` may optionally be qualified
> with a schema name.

```sql
CREATE EXTERNAL TABLE <table-name>
  FROM snowflake
  OPTIONS (
    account_name = '<account-name>',
    login_name = '<login-name>',
    password = '<password>',
    database_name = '<database_name>',
    warehouse = '<warehouse>',
    role_name = '<role-name>',
    schema_name = '<schema-name>',
    table_name = '<table-name>',
  );
```

### External table long format options

| Field           | Description                                               |
|-----------------|-----------------------------------------------------------|
| `account-name`  | Account containing the Snowflake warehouse to connect to. |
| `login-name`    | Name of the user to login as.                             |
| `password`      | Password for the above user.                              |
| `database-name` | Name of the database to connect to.                       |
| `warehouse`     | Name of the warehouse to connect to.                      |
| `role-name`     | Role to use when connecting.                              |
| `schema-name`   | The name of the schema where the table resides            |
| `table-name`    | The name of the table                                     |

<!-- markdownlint-disable line-length -->

[CREATE EXTERNAL TABLE]: {{site.baseurl}}/docs/sql-commands/create-external-table
[CREATE EXTERNAL DATABASE]: {{site.baseurl}}/docs/sql-commands/create-external-database

<!-- markdownlint-enable line-length -->

