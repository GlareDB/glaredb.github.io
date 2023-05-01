---
layout: default
title: Postgres
parent: Supported data sources
grand_parent: Data sources
---

# Postgres

Postgres is able to be used as an external data source. Either an entire
database or a single table may be added as a data source.

## External database

An entire Postgres database can be added using the [CREATE EXTERNAL DATABASE]
command.

{: .important}

> There are two equivalent formats. In both formats, `database-name` will be the
> name of the database inside GlareDB. This cannot be qualified, and must be
> unique across all other databases in the deployment.

### External database long format

```sql
CREATE EXTERNAL DATABASE <database-name>
 FROM postgres
 OPTIONS (
  host = '<host>',
  port = '<port>',
  user = '<user>',
  password = '<password>',
  database = '<database>',
 );
```

### External database long format options

| Field      | Description                                        |
| ---------- | -------------------------------------------------- |
| `host`     | The host that the postgres service is available on |
| `port`     | The port the postgres database is available on     |
| `user`     | A database role with login (see [CREATE USER])     |
| `password` | The password associated to the above `user`        |
| `database` | The name of the database (see [CREATE DATABASE])   |

### External database compact format

```sql
CREATE EXTERNAL DATABASE <database-name>
 FROM postgres
 OPTIONS (
  connection_string = '<connection-string>',
 );
```

### External database compact format options

| Field               | Description                                                                |
| ------------------- | -------------------------------------------------------------------------- |
| `connection_string` | Key value string containing connection details (see [Connection Strings]). |

## External table

Adding an external table can be done through the [CREATE EXTERNAL TABLE]
command.

{: .important}

> There are two equivalent foramts. In both formats, `table-name` will be the
> name of the database inside GlareDB. `table-name` may optionally be qualified
> with a schema name.

### External table long format

```sql
CREATE EXTERNAL TABLE <table-name>
 FROM postgres
 OPTIONS (
  host = '<host>',
  port = '<port>',
  user = '<user>',
  password = '<password>',
  database = '<database>',
  schema = '<schema>',
  table = '<table>',
);
```

#### External table long format options

| Field      | Description                                                          |
| ---------- | -------------------------------------------------------------------- |
| `host`     | The host that the postgres service is available on                   |
| `port`     | The port the postgres database is available on                       |
| `user`     | A database role with login (see [CREATE USER])                       |
| `password` | The password associated to the above `user`                          |
| `database` | The name of the database (see [CREATE DATABASE])                     |
| `schema`   | The name of the schema where the table resides (see [CREATE SCHEMA]) |
| `table`    | The name of the table (see [CREATE TABLE])                           |

### External table compact format

```sql
CREATE EXTERNAL TABLE <table-name>
 FROM postgres
 OPTIONS (
  connection_string = '<connection-string>',
  schema = '<schema>',
  table = '<table>',
 );
```

#### External table compact format options

| Field               | Description                                                                |
| ------------------- | -------------------------------------------------------------------------- |
| `connection_string` | Key value string containing connection details (see [Connection Strings]). |
| `schema`            | The name of the schema where the table resides (see [CREATE SCHEMA])       |
| `table`             | The name of the table (see [CREATE TABLE])                                 |

<!-- markdownlint-disable line-length -->

[CREATE EXTERNAL TABLE]: /docs/sql-reference/sql-commands/create-external-table
[CREATE EXTERNAL DATABASE]: /docs/sql-reference/sql-commands/create-external-database
[CREATE USER]: https://www.postgresql.org/docs/current/sql-createuser.html
[CREATE DATABASE]: https://www.postgresql.org/docs/current/sql-createdatabase.html
[CREATE SCHEMA]: https://www.postgresql.org/docs/current/sql-createschema.html
[CREATE TABLE]: https://www.postgresql.org/docs/current/sql-createtable.html
[Connection Strings]: https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-CONNSTRING

<!-- markdownlint-enable line-length -->
