---
title: Why GlareDB?
layout: default
parent: What is GlareDB?
nav_order: 1
---

<!-- markdownlint-disable title-case-style -->

# Why GlareDB?

<!-- markdownlint-enable title-case-style -->

GlareDB is designed to make **time to first insight** as quick as possible.
Instead of having to rely on ETL (Extract-Transform-Load) pipelines to move data
across databases, GlareDB hooks directly into your data sources. With GlareDB,
you no longer have to wait on an ETL pipeline before being able to work on the
freshest data.

## Simple interface

GlareDB gracefully plugs into your stack and allows you to use the languages and
tools you already know.

### Example

> **Note**: To learn about the data sources we support, refer to
> [data sources documentation](../data-sources/index.md).

The example below uses `psql` to perform the following steps:

1. Connect GlareDB to a PostgreSQL database named `my_db`
2. Query a table `animals` on `my_db`

Connecting:

```console
psql "postgresql://user:password@proxy.glaredb.com:6543/my_db"
```

Response:

```console
my_db=>
```

Connecting GlareDB to `my_db`:

> **Note**: This only needs to be done once. `my_db` will be recognized as a
> data source for future sessions and queries, unless it is explicitly removed.

```sql
CREATE EXTERNAL DATABASE pg_db
  FROM postgres
  OPTIONS (
    host = 'localhost',
    port = '5432',
    user = 'postgres',
    password = 'postgres',
    database = 'postgres',
);
```

Response:

```console
CREATE DATABASE
```

Querying `my_db`:

```sql
SELECT * from pg_db.public.animals
```

Response:

```console
 animal
--------
 dog
 cat
 monkey
(3 rows)
```
