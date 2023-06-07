---
layout: default
title: Connecting data sources
parent: Data sources
---

# Connecting data sources

## Connecting data sources using GlareDB Cloud

[Learn more about managing data sources in GlareDB Cloud].

## Connecting data sources using SQL

Data sources can be added using [CREATE EXTERNAL TABLE] or
[CREATE EXTERNAL DATABASE].

To add a **Postgres** data source using the [CREATE EXTERNAL DATABASE] command.

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

When we submit this command, validation is done to ensure we can properly
connect. Any errors connecting will be returned, for example:

```text
ERROR:  External database validation failed: Failed to connect to Postgres
instance: error connecting to server: Connection refused (os error 111)
```

If everything validates and no errors are returned, the data source is then
available to query from within the deployment.

[Learn more about managing data sources in GlareDB Cloud]: /cloud/data-sources/index/
[CREATE EXTERNAL DATABASE]: /docs/sql-reference/sql-commands/create-external-database
[CREATE EXTERNAL TABLE]: /docs/sql-reference/sql-commands/create-external-table
