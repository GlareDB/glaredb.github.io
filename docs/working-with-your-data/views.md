---
layout: default
title: Saving your queries as views
parent: "Step 2: Work with your data"
---

# Saving your queries as views

Any valid `SELECT` query can be used when defining a view. You can leverage this
to save complicated queries that pull from multiple data sources as a simple
view.

The query defined [in the previous section] can be turned into a view with no
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

## Saving your queries as views in GlareDB Cloud

GlareDB Cloud has an integrated SQL workspace that can be used to one-click save
a query as a view. For more information refer to
[Save queries as views in GlareDB Cloud].

[in the previous section]: /docs/working-with-your-data/querying.html#querying-multiple-data-sources
[Save queries as views in GlareDB Cloud]: /cloud/data-sources/views-and-results/#save-queries-as-views
[CREATE VIEW]: /glaredb/sql-commands/create-view
