---
layout: default
title: Querying your data source
parent: Managing data sources
nav_order: 2
---

# Querying your data sources in GlareDB Cloud

GlareDB Cloud has an integrated SQL workspace that can be used to connect, query
and manage data sources.

From the main page, select the deployment you wish to query.

![Organization deployment list]

![Deployment overview]

Then click the **SQL Workspace** navigation at the top to access the SQL
workspace. Here you can run queries, see previously run queries, extract results
and save queries as views.

![SQL workspace]

## Query syntax

Querying your data sources in GlareDB is simple. You can use familiar `SELECT`
and `JOIN` statements. External tables do not need to be qualified. Tables on
external databases require qualification.

For example, the following query for accesses an external database named
`example` with a `public` schema containing a `users` table:

```sql
SELECT * FROM example.public.users;
```

For more information, refer to our guide on [Working with your data] and the
[SQL commands reference].

## Use your preferred Postgres client

You can connect to GlareDB with your preferred Postgres-compatible clients,
such as `psql`. For more information on connections strings and passwords, refer
to [Connection Details] and [Managing Passwords].

[Organization deployment list]: /assets/images/org-deployments.png
[Deployment overview]: /assets/images/deployment-overview.png
[SQL workspace]: /assets/images/sql_workspace.png
[Working with your data]: /docs/working-with-your-data/
[SQL commands reference]: /glaredb/sql-commands/index/
[Connection Details]: /cloud/access/connection-details/
[Managing Passwords]: /cloud/access/managing-passwords/
