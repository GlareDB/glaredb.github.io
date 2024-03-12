---
title: Key Concepts
layout: default
nav_order: 1
parent: Introduction / Getting Started
---

# Key Concepts in GlareDB

## Table Functions

A core tenet of GlareDB is that [All Data are SQL Addressable], even data not
in a SQL database.

Table functions access data, on-demand, wherever it is, including data sources
that have not been added to GlareDB.

Local _and_ remote files can be read with functions such as:

<!-- TODO: add links -->

- `read_bson`
- `read_clickhouse`
- `read_csv`
- `read_execel`
- `read_json`
- `read_parquet`

Database tables can be read with functions such as:

- `read_bigquery`
- `read_mongodb`
- `read_mysql`
- `read_postgres`
- `read_snowflake`
- `read_sqlserver`

Data lake table formats can be read with:

- `read_delta`
- `read_iceberg`

All of these table functions can be mixed and matched in queries with tables
and all other supported SQL functions.

For example:

```sql
SELECT * FROM my_table m
INNER JOIN read_csv('./my_csv') c ON m.id = c.id;
```

## External Data Sources

In a typical "modern data stack", data is extracted and transformed from various
sources and loaded into an analytics warehouse. The assumption of these is that
analytics should own storage and infrastructure, often at great complexity.

GlareDB shifts the dynamic by recognizing that data is accessible where it is,
for example with table functions. However, it is often the case that the same
sources are accessed frequently and benefit from being recognized as known
sources.

This is where external data sources shine: tables and entire databases can be
added to GlareDB. By cataloging your data with GlareDB, it is accessible
wherever you use GlareDB, including applications, notebooks, data dashboards
and more.

The following adds an entire Postgres database to GlareDB's catalog, so that the
data can be accessed using `my_pg.schema.table`. Note that the data is not
imported/stored in GlareDB: it still resides in the external system and can
be accessed on-demand.

```sql
CREATE EXTERNAL DATABASE my_pg FROM postgres OPTIONS (
    host = 'my_host',
    port = '5432',
    user = 'postgres',
    password = 'postgres'
)
```

A heuristic is to use table functions for:

- Querying local, scratch or exploratory data
- One-offs or infrequent queries

and add external data sources for the remaining cases.

## Native Data Storage

## Hybrid Execution

## Remote Execution

## Serverless Native

[All Data are SQL Addressable]: https://glaredb.com/blog/explain-glaredb-to-your-friends
