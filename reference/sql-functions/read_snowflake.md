---
layout: default
title: read_snowflake
parent: SQL functions
grand_parent: Reference
---

# `read_snowflake`

Read a table residing in a Snowflake warehouse. The table does not have to be a
known data source to GlareDB.

## Syntax

```sql
read_snowflake(
  <account>,
  <username>,
  <password>,
  <database>,
  <warehouse>,
  <role>,
  <schema>,
  <table>
)
```

| Field       | Description                                               |
| ----------- | --------------------------------------------------------- |
| `account`   | Account containing the Snowflake warehouse to connect to. |
| `username`  | Name of the user to login as.                             |
| `password`  | Password for the above user.                              |
| `database`  | Name of the database to connect to.                       |
| `warehouse` | Name of the warehouse to connect to.                      |
| `role`      | Role to use when connecting.                              |
| `schema`    | The name of the schema.                                   |
| `table`     | The name of the table to query.                           |

## Examples

In the following example, a 'users' table located in a Snowflake warehouse is
queryed.

```sql
select * from read_snowflake(
  'xy12345',
  'snowflake_username',
  'snowflake_password',
  'my_database',
  'my_warehouse',
  'USERADMIN',
  'public',
  'users'
);
```

Refer to the [documentation on Snowflake data sources] for more information.

[documentation on Snowflake data sources]: /docs/data-sources/supported/snowflake
