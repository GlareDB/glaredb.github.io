---
layout: default
title: 2. Work with your data
nav_order: 3
---

<!-- markdownlint-disable MD022 -->

<!-- prettier-ignore-start -->
# Working with your data
{: .no_toc }
<!-- prettier-ignore-end -->

<!-- markdownlint-enable MD022 -->

After setting up some [data sources], it's time to begin querying your data.
GlareDB is designed to run analytical queries that access data from multiple
sources, and writing SQL queries that reference multiple sources is easy.

<!-- prettier-ignore -->
- TOC
{:toc}



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
