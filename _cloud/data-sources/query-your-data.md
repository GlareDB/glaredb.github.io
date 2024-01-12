---
layout: default
title: Querying your data source
parent: Managing data sources
nav_order: 2
---

# Querying your data sources in GlareDB Cloud

GlareDB Cloud has an integrated SQL workspace that can be used to connect, query
and manage data sources. From the main page, click the **SQL workspace** link
for a deployment.

![Deployment list]

The SQL workspace contains various helpful features for exploring your data,
querying your data and producing basic reports:

- Schema explorer and search (available from the sidebar)
- Recent queries (available from the sidebar)
- Completion hints for tables and functions (available in the editor)
- Exporting results (available from the results panel)

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

## Hybrid Execution

You can connect to your GlareDB Cloud deployment locally using [Hybrid Execution].
[Hybrid Execution] is available in the GlareDB CLI as well as the
[GlareDB Python library].

## Use your preferred Postgres client

You can connect to GlareDB with your preferred Postgres-compatible clients,
such as `psql`. For more information on connections strings and passwords, refer
to [Connection Details] and [Managing Passwords].

[Deployment list]: /assets/images/cloud/data-sources/deployments-list.png
[SQL workspace]: /assets/images/cloud/data-sources/sql_workspace.png
[Hybrid Execution]: /glaredb/hybrid-execution
[GlareDB Python library]: /glaredb/python/
[Working with your data]: /docs/working-with-your-data/
[SQL commands reference]: /glaredb/sql-commands/index/
[Connection Details]: /cloud/access/connection-details/
[Managing Passwords]: /cloud/access/managing-passwords/
