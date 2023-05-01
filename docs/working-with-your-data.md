---
layout: default
title: Working with your data
nav_order: 5
---

# Working with your data
{: .no_toc }

After setting up some [data sources], it's time to begin querying your data.
GlareDB is designed to run analytical queries that access data from multiple
sources, and writing SQL queries that reference multiple sources is easy.

- TOC
{:toc}

## Referencing data sources in queries

Data sources are either external tables (see [CREATE EXTERNAL TABLE]) or
external database (see [CREATE EXTERNAL DATABASE]). Getting a list of data
sources connected to your deployment can be done with the following SQL query.

```sql
my_deployment=> select datasource, name, object_type from glare_catalog.external_datasources;
 datasource | name  | object_type
------------+-------+-------------
 postgres   | users | table
 bigquery   | bq    | database
 mongo      | atlas | database
 postgres   | qa    | database
(4 rows)
```

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
my_deployment=> select datasource, name, object_type from glare_catalog.external_datasources;
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

## Creating views referencing data sources

Any valid SELECT query can be used when defining a view. This enables us to
create a view that can reference any number of data sources.

The query defined in the previous section can be turned into a view with no
changes:

```sql
create view num_deployments_created_after_upgrade(num_deployments, org_id) as (
  select count(*), o.id
    from bq.events.billing_plan_upgraded as b
         inner join prod.public.organizations as o on b.org_id = o.id
         inner join prod.public.deployments as d on o.id = d.org_id
   where d.created_at > b.timestamp
   group by o.id)
```

And now we're able to query the view without having to specify individual data
sources to query.

```sql
select * from num_deployments_created_after_upgrade;
```

Using views to define queries that reference multiple data sources is a powerful
way of modeling data for use in upstream clients and applications. A single view
could be used for generating a report in Tableau and also be accessible in
`psql` or other tools.

See [CREATE VIEW] for the reference doc on views.

[data sources]: /docs/data-sources/overview
[CREATE EXTERNAL DATABASE]: /docs/sql-reference/sql-commands/create-external-database
[CREATE EXTERNAL TABLE]: /docs/sql-reference/sql-commands/create-external-table
[CREATE VIEW]: /docs/sql-reference/sql-commands/create-view
