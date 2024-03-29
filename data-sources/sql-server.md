---
layout: default
title: SQL Server
parent: Data Sources
---

<!-- markdownlint-disable MD022 -->

<!-- prettier-ignore-start -->
# SQL Server
{: .no_toc }
<!-- prettier-ignore-end -->

<!-- markdownlint-enable MD022 -->

GlareDB supports SQL Server as an external data source. You can configure single
tables and entire databases from SQL Server.

<!-- prettier-ignore-start -->

- TOC
{:toc}
<!-- prettier-ignore-end -->

## Add a SQL Server Database

Add an entire SQL Server database with the [CREATE EXTERNAL DATABASE]
command.

{: .important}

> `<database-name>` will be the name of the database in GlareDB.
> This cannot be qualified, and must be unique across all other
> databases in the deployment.

### Database Format

```sql
CREATE EXTERNAL DATABASE <database-name>
 FROM sql_server
 OPTIONS (
   connection_string = '<connection_string>'
 );
```

### Database Options

| Field               | Description                                                    |
| ------------------- | -------------------------------------------------------------- |
| `connection_string` | An [ADO connection string] pointing to the SQL Server instance |

## Add a Single Table

Add an external table with the [CREATE EXTERNAL TABLE]
command.

{: .important}

> `table-name` becomes the name of the database in GlareDB. `table-name` may be qualified
> with a schema name.

### Table format

```sql
CREATE EXTERNAL TABLE <table-name>
 FROM sql_server
 OPTIONS (
  connection_string = '<connection_string>',
  schema = '<schema>',
  table = '<table>'
);
```

### Table Options

| Field               | Description                                                    |
| ------------------- | -------------------------------------------------------------- |
| `connection_string` | An [ADO connection string] pointing to the SQL Server instance |
| `schema`            | The name of the schema where the table resides                 |
| `table`             | The name of the table                                          |

<!-- markdownlint-disable line-length -->

[CREATE EXTERNAL TABLE]: /reference/sql-commands/create-external-table
[CREATE EXTERNAL DATABASE]: /reference/sql-commands/create-external-database
[ADO connection string]: https://learn.microsoft.com/en-us/dotnet/framework/data/adonet/connection-string-syntax#sql-server-authentication-with-sqlclient

<!-- markdownlint-enable line-length -->
