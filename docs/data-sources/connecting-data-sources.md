---
layout: default
title: Connecting data sources
parent: "Step 1: Connect your data sources"
---

# Connecting data sources

Connect your data sources with GlareDB and GlareDB Cloud.

## Connecting data sources using SQL

Data sources can be added using [CREATE EXTERNAL TABLE] or
[CREATE EXTERNAL DATABASE].

[See all supported data sources].

### Example: Postgres data source

A **Postgres** database can be added using [CREATE EXTERNAL DATABASE]:

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

Upon command execution, the connection is immediately validated. Any errors
connecting will be returned, for example:

```text
ERROR:  External database validation failed: Failed to connect to Postgres
instance: error connecting to server: Connection refused (os error 111)
```

If everything validates and no errors are returned, the data source is then
available to query from within the deployment. The data source will not be saved
if validation fails.

## Connecting data sources using GlareDB Cloud

[Learn more about managing data sources in GlareDB Cloud].

[CREATE EXTERNAL DATABASE]: /docs/sql-reference/sql-commands/create-external-database
[CREATE EXTERNAL TABLE]: /docs/sql-reference/sql-commands/create-external-table
[See all supported data sources]: /docs/data-sources/supported/
[Learn more about managing data sources in GlareDB Cloud]: /cloud/data-sources/index/
