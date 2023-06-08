---
layout: default
title: MySQL
parent: Supported data sources
grand_parent: "Step 1: Connect your data sources"
---

<!-- markdownlint-disable MD022 -->

<!-- prettier-ignore-start -->
# MySQL
{: .no_toc }
<!-- prettier-ignore-end -->

<!-- markdownlint-enable MD022 -->

MySQL is able to be used as an external data source. Either an entire database
or a single table may be added as a data source.

- TOC
{:toc}

## Connect a MySQL database

An entire MySQL database can be added using the [CREATE EXTERNAL DATABASE]
command.

{: .important}

> There are two equivalent formats. In both formats, `database-name` will be the
> name of the database inside GlareDB. This cannot be qualified, and must be
> unique across all other databases in the deployment.

### Database long format

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

### Database long format options

| Field         | Description                                     |
| ------------- | ----------------------------------------------- |
| `tunnel-name` | The name of the SSH tunnel to connect with      |
| `host`        | The host that the MySQL service is available on |
| `port`        | The port the MySQL database is available on     |
| `user`        | A MySQL database user                           |
| `password`    | The password associated to the above `user`     |
| `database`    | The name of the database                        |

### Database compact format

```sql
CREATE EXTERNAL DATABASE <database-name>
 FROM mysql
 [TUNNEL <tunnel-name>]
 OPTIONS (
  connection_string = '<connection-string>',
 );
```

### Database compact format options

| Field               | Description                                                              |
| ------------------- | ------------------------------------------------------------------------ |
| `tunnel-name`       | The name of the SSH tunnel to connect with                               |
| `connection_string` | A mysql connection string, e.g. `mysql://user:password@myhost:3307/mydb` |

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

### Table long format options

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

### Table compact format

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

### Table compact format options

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
