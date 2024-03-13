---
title: Key Concepts
layout: default
nav_order: 1
parent: Getting Started
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
sources and loaded into an analytics warehouse. An underlying assumption is
analytics should own storage and infrastructure, often at great complexity.

GlareDB provides access to data where it is, without requiring a move.
Even though data is more dynamic, having data sources configured in GlareDB 
makes it easier to access common data sources and share configuration between
users.

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

In addition to reading files and external data sources, GlareDB has native
storage. Tables can be created and data can be inserted, updated, and deleted as
needed.

```sql
CREATE TABLE my_table (
    a_column TEXT
);

INSERT INTO my_table VALUES ('hello world');

DELETE FROM my_table;
```

## Hybrid Execution

Often, workloads with GlareDB start locally in the [CLI] or with language
bindings such as [Python] and [Node.js]. In these workloads, GlareDB runs on
a local machine either entirely in-memory with no persistence after the process
exits, or with local persistence.

[GlareDB Cloud] extends and scales these workflows. By connecting local clients
to [GlareDB Cloud], queries are partitioned and optimized to run both in-process
and using cloud compute. Data can be accessed and stored in cloud and shared
with your team. When using [GlareDB Cloud], your can access your data in all of
your applications.

## Remote Execution

GlareDB is compatible with the Postgres protocol, meaning that tools used to
connect to Postgres can be used with GlareDB. For example, `lib/pq` in a Go
application.

When connecting via the Postgres protocol, all execution occurs in GlareDB. For
example if using [GlareDB Cloud], queries will not be hybrid: all execution
occurs in the cloud.

## Serverless Native

GlareDB is built from the bottom up with serverless operation and delivery in mind.
Storage and compute are separated and can be scaled independently, and all billing 
is based on data processed (not time!) so users only pay for the resources they use.

By designing the system this way, our billing system is consumption-based and
transparent. We bill for bytes processed and bytes stored, rather than resource
or time-based metrics. Billing on these metrics means that queries can get
faster, spanning multiple worker nodes and various compute resources without
the end-user incurring any change in cost!

For more information, read our [announcement post on GlareDB Pro].

[All Data are SQL Addressable]: https://glaredb.com/blog/explain-glaredb-to-your-friends
[GlareDB Cloud]: https://console.glaredb.com
[CLI]: /introduction/installation/locally-cli.html
[Python]: /introduction/installation/python-bindings.html
[Node.js]: /introduction/installation/node_bindings.html
[announcement post on GlareDB Pro]: https://glaredb.com/blog/glaredb-pro-release-announcement
