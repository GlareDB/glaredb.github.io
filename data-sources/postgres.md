---
layout: default
title: Postgres
parent: Data Sources
---

<!-- markdownlint-disable MD022 -->

<!-- prettier-ignore-start -->
# Postgres
{: .no_toc }
<!-- prettier-ignore-end -->

<!-- markdownlint-enable MD022 -->

Postgres is able to be used as an external data source. Either an entire
database or a single table may be added as a data source.

<!-- prettier-ignore-start -->

- TOC
{:toc}
<!-- prettier-ignore-end -->

## Connect a Postgres database

An entire Postgres database can be added using the [CREATE EXTERNAL DATABASE]
command.

{: .important}

> There are two equivalent formats. In both formats, `database-name` will be the
> name of the database inside GlareDB. This cannot be qualified, and must be
> unique across all other databases in the deployment.

### Database long format

```sql
CREATE EXTERNAL DATABASE <database-name>
 FROM postgres
 [TUNNEL <tunnel-name>]
 OPTIONS (
  host = '<host>',
  port = '<port>',
  user = '<user>',
  password = '<password>',
  database = '<database>',
 );
```

### Database long format options

| Field         | Description                                        |
| ------------- | -------------------------------------------------- |
| `tunnel-name` | The name of the SSH tunnel to connect with         |
| `host`        | The host that the postgres service is available on |
| `port`        | The port the postgres database is available on     |
| `user`        | A database role with login (see [CREATE USER])     |
| `password`    | The password associated to the above `user`        |
| `database`    | The name of the database (see [CREATE DATABASE])   |

### Database compact format

```sql
CREATE EXTERNAL DATABASE <database-name>
 FROM postgres
 [TUNNEL <tunnel-name>]
 OPTIONS (
  connection_string = '<connection-string>',
 );
```

### Database compact format options

| Field               | Description                                                                |
| ------------------- | -------------------------------------------------------------------------- |
| `tunnel-name`       | The name of the SSH tunnel to connect with                                 |
| `connection_string` | Key value string containing connection details (see [Connection Strings]). |

## Connect a single table

Adding an external table can be done through the [CREATE EXTERNAL TABLE]
command.

{: .important}

> There are two equivalent formats. In both formats, `table-name` will be the
> name of the database inside GlareDB. `table-name` may optionally be qualified
> with a schema name.

### Table long format

```sql
CREATE EXTERNAL TABLE <table-name>
 FROM postgres
 [TUNNEL <tunnel-name>]
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

### Table long format options

| Field         | Description                                                          |
| ------------- | -------------------------------------------------------------------- |
| `tunnel-name` | The name of the SSH tunnel to connect with                           |
| `host`        | The host that the postgres service is available on                   |
| `port`        | The port the postgres database is available on                       |
| `user`        | A database role with login (see [CREATE USER])                       |
| `password`    | The password associated to the above `user`                          |
| `database`    | The name of the database (see [CREATE DATABASE])                     |
| `schema`      | The name of the schema where the table resides (see [CREATE SCHEMA]) |
| `table`       | The name of the table (see [CREATE TABLE])                           |

### Table compact format

```sql
CREATE EXTERNAL TABLE <table-name>
 FROM postgres
 [TUNNEL <tunnel-name>]
 OPTIONS (
  connection_string = '<connection-string>',
  schema = '<schema>',
  table = '<table>',
 );
```

### Table compact format options

| Field               | Description                                                                |
| ------------------- | -------------------------------------------------------------------------- |
| `tunnel-name`       | The name of the SSH tunnel to connect with                                 |
| `connection_string` | Key value string containing connection details (see [Connection Strings]). |
| `schema`            | The name of the schema where the table resides (see [CREATE SCHEMA])       |
| `table`             | The name of the table (see [CREATE TABLE])                                 |

<!-- markdownlint-disable line-length -->

[CREATE EXTERNAL TABLE]: /glaredb/sql-commands/create-external-table
[CREATE EXTERNAL DATABASE]: /glaredb/sql-commands/create-external-database
[CREATE USER]: https://www.postgresql.org/docs/current/sql-createuser.html
[CREATE DATABASE]: https://www.postgresql.org/docs/current/sql-createdatabase.html
[CREATE SCHEMA]: https://www.postgresql.org/docs/current/sql-createschema.html
[CREATE TABLE]: https://www.postgresql.org/docs/current/sql-createtable.html
[Connection Strings]: https://www.postgresql.org/docs/current/libpq-connect.html#LIBPQ-CONNSTRING

<!-- markdownlint-enable line-length -->
