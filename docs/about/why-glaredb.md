---
title: Why GlareDB?
layout: default
parent: What is GlareDB?
nav_order: 1
---

# Why GlareDB?

GlareDB is designed to make **time to first insight** as quick as possible.
Instead of having to rely on ETL pipelines to move data around, GlareDB hooks
directly into your data sources. With GlareDB, you no longer have to wait before
being able to work on the freshest data set.

## Simple interface

GlareDB gracefully plugs into your stack and allows you to use the languages and
tools you already know.

### Example: query an external Postgres database in 2 steps

The example below uses `psql` to perform the following steps:

1. Connect a GlareDB deployment named `gdb` to a PostgreSQL database
2. Query a table `public.animals` on the PostgreSQl database

Connecting:

```console
psql "postgresql://user:password@proxy.glaredb.com:6543/gdb"
gdb=>
```

Connecting GlareDB to a PostgreSQL database:

{: .important}

> This only needs to be done once. `pg_db` will be recognized as a data source
> for future sessions and queries, unless it is explicitly removed.

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

Querying `pg_db`:

```sql
SELECT * from pg_db.public.animals;
```

Response:

```console
 animal
--------
 cat
 dog
 monkey
(3 rows)
```

[Learn more about data sources].

[Learn more about data sources]: /docs/data-sources/index
