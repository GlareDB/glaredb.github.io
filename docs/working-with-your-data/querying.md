---
layout: default
title: Querying your data sources
parent: "Step 2: Work with your data"
---

<!-- markdownlint-disable MD022 -->

<!-- prettier-ignore-start -->
# Querying your data sources
{: .no_toc }
<!-- prettier-ignore-end -->

<!-- markdownlint-enable MD022 -->

Data sources are either external tables (see [CREATE EXTERNAL TABLE]) or
external database (see [CREATE EXTERNAL DATABASE]).

<!-- prettier-ignore-start -->

- TOC
{:toc}
<!-- prettier-ignore-end -->

## Listing data sources

Listing data sources connected to your deployment can be done with the following
SQL query:

```sql
SELECT datasource, name, object_type
FROM glare_catalog.external_datasources;
```

```text
 datasource | name  | object_type
------------+-------+-------------
 postgres   | users | table
 bigquery   | bq    | database
 mongo      | atlas | database
 postgres   | qa    | database
(4 rows)
```

## Qualifying data sources

The `object_type` column indicates whether the data source is an external table
or an external database. In this example, there's three external databases and
one external table.

When a data source is an external table, it may be queried with just its name.
For example, querying the data source named `users`:

```sql
select * from users;
```

When a data source is an external database, a fully qualified name must be used
to reference the table of interest. For example, querying an `account_signup`
table inside a `events` schema in the `bq` data source:

```sql
select * from bq.events.account_signup;
```

## Querying multiple data sources

The real power of GlareDB is being able to work with multiple data sources in a
single query. Let's work through an example using a BigQuery and Postgres data
source.

```sql
select datasource, name, object_type
from glare_catalog.external_datasources;
```

```text
 datasource | name  | object_type
------------+-------+-------------
 bigquery   | bq    | database
 postgres   | prod  | database
(2 rows)
```

Internally at GlareDB, we want to be able be able to answer the question "How
many GlareDB deployments were created per organization after the organization
has upgraded their billing plan?"

Our production Postgres holds information about deployments and organizations,
and our BigQuery instance stores all events about _when_ things happened. So to
answer this question, we can join a table from our BigQuery data source onto
tables inside our Postgres data source:

```sql
select count(*) as num_deployments, o.id
  from bq.events.billing_plan_upgraded as b
       inner join prod.public.organizations as o on b.org_id = o.id
       inner join prod.public.deployments as d on o.id = d.org_id
 where d.created_at > b.timestamp
 group by o.id
```

Notice we're able reference data sources everywhere you would normally reference
tables in a typically SQL database.

## Querying data sources with GlareDB Cloud

GlareDB Cloud has an integrated SQL workspace. For more information refer to
[Querying your data sources in GlareDB Cloud].

[CREATE EXTERNAL DATABASE]: /glaredb/sql-commands/create-external-database
[CREATE EXTERNAL TABLE]: /glaredb/sql-commands/create-external-table
[Querying your data sources in GlareDB Cloud]: /cloud/data-sources/query-your-data/
