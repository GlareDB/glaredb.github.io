---
title: Data Sources
layout: home
nav_order: 2
has_children: true
---

# Data sources

GlareDB can connect to a broad range of external data sources so that you readily
query your data and join them together no matter where they live.

## Supported data sources

* [Azure]
* [BigQuery]
* [Clickhouse]
* [GCS]
* [MongoDB]
* [MySQL]
* [Postgres]
* [S3]
* [SQL Server]
* [Snowflake]

## Connecting data sources using SQL

Define new data sources with [CREATE EXTERNAL TABLE] or [CREATE
EXTERNAL DATABASE]. You can add new data sources to a GlareDB instance
at any time. There are no restrictions on the number of data sources you can configure.

### Example: Postgres data source

Add a **Postgres** database to GlareDB [CREATE EXTERNAL DATABASE]:

```sql
glare=> CREATE EXTERNAL DATABASE external_db
    FROM postgres
    OPTIONS (
        host = 'my.postgres.host',
        port = '5432',
        user = 'glaredb',
        password = 'password',
        database = 'glaredb_test',
    );
```

This operation creates an entry in the GlareDB catalog for the
Postgres database `glaredb_test` which is accessible as
`external_db`. All of the tables and resources within this Postgres
database are now addressable by GlareDB queries.

GlareDB validates the connection when you create the external
database and returns any error immediately, as in:

```text
ERROR:  External database validation failed: Failed to connect to Postgres
instance: error connecting to server: Connection refused (os error 111)
```

If there are no validation errors, the data source is available to
query from within the deployment. GlareDB will not save invalid data
sources.

## Connecting data sources using GlareDB Cloud

[CREATE EXTERNAL DATABASE]: /glaredb/sql-commands/create-external-database
[CREATE EXTERNAL TABLE]: /glaredb/sql-commands/create-external-table
[Azure]: ./azure
[BigQuery]: ./bigquery
[Clickhouse]: ./clickhouse
[GCS]: ./gcs
[MongoDB]: ./mongodb
[MySQL]: ./mysql
[Postgres]: ./postgres
[S3]: ./s3
[SQL Server]: ./sql-server
[Snowflake]: ./snowflake
