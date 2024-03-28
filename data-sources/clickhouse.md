---
layout: default
title: ClickHouse
parent: Data Sources
---

<!-- markdownlint-disable MD022 -->

<!-- prettier-ignore-start -->
# ClickHouse
{: .no_toc }
<!-- prettier-ignore-end -->

<!-- markdownlint-enable MD022 -->

ClickHouse is able to be used as an external data source. Either an entire
database or a single table may be added as a data source.

<!-- prettier-ignore-start -->

- TOC
{:toc}
<!-- prettier-ignore-end -->

## Connect a ClickHouse database

An entire ClickHouse database can be added using the [CREATE EXTERNAL DATABASE]
command.

{: .important}

### Database

```sql
CREATE EXTERNAL DATABASE <database-name>
 FROM clickhouse
 OPTIONS (
  connection_string = '<connection-string>',
 );
```

### Database options

| Field               | Description                                                                    |
| ------------------- | ------------------------------------------------------------------------------ |
| `connection-string` | The connection string to use when connecting to an external ClickHouse server. |

The connection string should be in the form `clickhouse://user:password@hostname:9000/database`.

Once connected, tables can be referenced with the format
`<glaredb-database>.<clickhouse-database>.<table>`.

#### External database example

```sql
-- Create a database with the name 'my_ch'.
CREATE EXTERNAL DATABASE my_ch
 FROM clickhouse
 OPTIONS (
  connection_string = 'clickhouse://my_user:my_password@my.clickhouse.host:9000/default'
 );

-- Query a table 'users' in the 'default' ClickHouse database.
SELECT * FROM my_ch.default.users;
```

## Connect a single table

To add an external table, use the [CREATE EXTERNAL TABLE] command. This will add
the table in the current schema.

### Table

```sql
CREATE EXTERNAL TABLE <table-name>
 FROM clickhouse
 OPTIONS (
  connection_string = '<connection-string>',
  table = '<table>'
);
```

### Table options

| Field               | Description                                                                    |
| ------------------- | ------------------------------------------------------------------------------ |
| `connection-string` | The connection string to use when connecting to an external ClickHouse server. |
| `table`             | The name of the table inside ClickHouse.                                       |

#### External table example

```sql
-- Create a table with the name 'ch_users'
-- backed by a 'users' table in ClickHouse.
CREATE EXTERNAL TABLE ch_users
 FROM clickhouse
 OPTIONS (
  connection_string = 'clickhouse://my_user:my_password@my.clickhouse.host:9000/default',
  table = 'users'
 );

-- Query a table 'ch_users'.
SELECT * FROM ch_users;
-- Qualified with the GlareDB schema.
SELECT * FROM public.ch_users;
```

<!-- markdownlint-disable line-length -->

[CREATE EXTERNAL TABLE]: /glaredb/sql-commands/create-external-table
[CREATE EXTERNAL DATABASE]: /glaredb/sql-commands/create-external-database

<!-- markdownlint-enable line-length -->
