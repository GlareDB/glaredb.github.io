---
layout: default
title: Connecting data sources
parent: "Step 1: Connect your data sources"
---

# Connecting data sources

Connect your data sources with GlareDB and GlareDB Cloud.

## Connecting data sources using SQL

Define new data sources with [CREATE EXTERNAL TABLE] or [CREATE
EXTERNAL DATABASE]. You can add new data sources to a GlareDB instance
at any time. There are no restrictions on the number of data sources you can configure.

[See all supported data sources].

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

[Learn more about managing data sources in GlareDB Cloud].

[CREATE EXTERNAL DATABASE]: /glaredb/sql-commands/create-external-database
[CREATE EXTERNAL TABLE]: /glaredb/sql-commands/create-external-table
[See all supported data sources]: /docs/data-sources/supported/
[Learn more about managing data sources in GlareDB Cloud]: /cloud/data-sources/index/
