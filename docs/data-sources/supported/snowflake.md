---
layout: default
title: Snowflake
parent: Supported data sources
grand_parent: "Step 1: Connect your data sources"
---

<!-- markdownlint-disable MD022 -->

<!-- prettier-ignore-start -->
# Snowflake
{: .no_toc }
<!-- prettier-ignore-end -->

<!-- markdownlint-enable MD022 -->

Snowflake is able to be used as an external data source. Either an entire
database or a single table may be added as a data source.

- TOC
{:toc}

## Connect a Snowflake database

An entire Snowflake database can be added using the [CREATE EXTERNAL DATABASE]
command.

{: .important}

> There are two equivalent formats. In both formats, `database-name` will be the
> name of the database inside GlareDB. This cannot be qualified, and must be
> unique across all other databases in the deployment.

### Database format

```sql
CREATE EXTERNAL DATABASE <database-name>
  FROM snowflake
  OPTIONS (
    account = '<account>',
    username = '<username>',
    password = '<password>',
    database = '<database>',
    warehouse = '<warehouse>',
    role = '<role>',
  );
```

### Database format options

| Field       | Description                                               |
| ----------- | --------------------------------------------------------- |
| `account`   | Account containing the Snowflake warehouse to connect to. |
| `username`  | Name of the user to login as.                             |
| `password`  | Password for the above user.                              |
| `database`  | Name of the database to connect to.                       |
| `warehouse` | Name of the warehouse to connect to.                      |
| `role`      | Role to use when connecting.                              |

## Connect a single table

Adding an external table can be done through the [CREATE EXTERNAL TABLE]
command.

{: .important}

> There are two equivalent formats. In both formats, `table-name` will be the
> name of the database inside GlareDB. `table-name` may optionally be qualified
> with a schema name.

### Table format

```sql
CREATE EXTERNAL TABLE <table-name>
  FROM snowflake
  OPTIONS (
    account = '<account>',
    username = '<username>',
    password = '<password>',
    database = '<database>',
    warehouse = '<warehouse>',
    role = '<role>',
    schema = '<schema>',
    table = '<table>',
  );
```

### Table format options

| Field       | Description                                               |
| ----------- | --------------------------------------------------------- |
| `account`   | Account containing the Snowflake warehouse to connect to. |
| `username`  | Name of the user to login as.                             |
| `password`  | Password for the above user.                              |
| `database`  | Name of the database to connect to.                       |
| `warehouse` | Name of the warehouse to connect to.                      |
| `role`      | Role to use when connecting.                              |
| `schema`    | The name of the schema where the table resides            |
| `table`     | The name of the table                                     |

<!-- markdownlint-disable line-length -->

[CREATE EXTERNAL TABLE]: /docs/sql-reference/sql-commands/create-external-table
[CREATE EXTERNAL DATABASE]: /docs/sql-reference/sql-commands/create-external-database

<!-- markdownlint-enable line-length -->
