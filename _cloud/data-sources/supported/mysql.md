---
layout: default
title: MySQL
parent: Supported data sources
grand_parent: Data sources
---

# MySQL

MySQL is able to be used as an external data source. Either an entire database
or a single table may be added as a data source.

## External database

An entire MySQL database can be added using the [CREATE EXTERNAL DATABASE]
command.

{: .important}

> There are two equivalent formats. In both formats, `database-name` will be the
> name of the database inside GlareDB. This cannot be qualified, and must be
> unique across all other databases in the deployment.

### External database long format

```sql
CREATE EXTERNAL DATABASE <database-name>
 FROM mysql
 [TUNNEL <tunnel-name>]
 OPTIONS (
  host = '<host>',
  port = '<port>',
  user = '<user>',
  password = '<password>',
  database = '<database>',
 );
```

### External database long format options

| Field         | Description                                     |
| ------------- | ----------------------------------------------- |
| `tunnel-name` | The name of the SSH tunnel to connect with      |
| `host`        | The host that the MySQL service is available on |
| `port`        | The port the MySQL database is available on     |
| `user`        | A MySQL database user                           |
| `password`    | The password associated to the above `user`     |
| `database`    | The name of the database                        |

### External database compact format

```sql
CREATE EXTERNAL DATABASE <database-name>
 FROM mysql
 [TUNNEL <tunnel-name>]
 OPTIONS (
  connection_string = '<connection-string>',
 );
```

### External database compact format options

| Field               | Description                                                              |
| ------------------- | ------------------------------------------------------------------------ |
| `tunnel-name`       | The name of the SSH tunnel to connect with                               |
| `connection_string` | A mysql connection string, e.g. `mysql://user:password@myhost:3307/mydb` |

## External table

Adding an external table can be done through the [CREATE EXTERNAL TABLE]
command.

{: .important}

> There are two equivalent formats. In both formats, `table-name` will be the
> name of the database inside GlareDB. `table-name` may optionally be qualified
> with a schema name.

### External table long format

```sql
CREATE EXTERNAL TABLE <table-name>
 FROM mysql
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

#### External table long format options

| Field         | Description                                     |
| ------------- | ----------------------------------------------- |
| `tunnel-name` | The name of the SSH tunnel to connect with      |
| `host`        | The host that the MySQL service is available on |
| `port`        | The port the MySQL database is available on     |
| `user`        | A MySQL database user                           |
| `password`    | The password associated to the above `user`     |
| `database`    | The name of the database                        |
| `schema`      | The name of the schema where the table resides  |
| `table`       | The name of the table                           |

### External table compact format

```sql
CREATE EXTERNAL TABLE <table-name>
 FROM MySQL
 [TUNNEL <tunnel-name>]
 OPTIONS (
  connection_string = '<connection-string>',
  schema = '<schema>',
  table = '<table>',
 );
```

#### External table compact format options

| Field               | Description                                    |
| ------------------- | ---------------------------------------------- |
| `tunnel-name`       | The name of the SSH tunnel to connect with     |
| `connection_string` | Key value string containing connection details |
| `schema`            | The name of the schema where the table resides |
| `table`             | The name of the table                          |

<!-- markdownlint-disable line-length -->

[CREATE EXTERNAL TABLE]: /docs/sql-reference/sql-commands/create-external-table
[CREATE EXTERNAL DATABASE]: /docs/sql-reference/sql-commands/create-external-database

<!-- markdownlint-enable line-length -->
