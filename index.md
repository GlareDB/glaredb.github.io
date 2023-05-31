---
title: What is GlareDB?
layout: home
nav_order: 1
has_children: true
---

# What is GlareDB?

GlareDB is a database that provides a single SQL interface for accessing your
data sources. With GlareDB you can query and join all of your data using just
SQL. No need for complex ETL pipelines to move data around before being able to
analyze it.

GlareDB is in [Technical Preview] and is generally available to everyone with
a free tier. Get started at [console.glaredb.com].

## What is a data source?

We currently support multiple databases and files in object storage. For
example, you can join data existing in a Postgres database with a CSV in S3
using basic SQL.

[Learn more about data sources]

## Where does GlareDB fit into your stack?

GlareDB sits between your data applications and your data sources. Any
application or client that can communicate using the Postgres protocol can
connect directly to GlareDB.

![Where GlareDB fits](/assets/images/where-glaredb-fits.png)

## Fully managed

Whether you use our serverless (free) or dedicated (paid plan) databases,
GlareDB is fully managed. With a few clicks, a GlareDB deployment will be ready
and highly available for you to use.

[Learn more about serverless and dedicated]

[Technical Preview]: ./docs/about/technical-preview.html
[console.glaredb.com]: https://console.glaredb.com
[Learn more about data sources]: ./docs/data-sources/
[Learn more about serverless and dedicated]: ./docs/deployments.html#dedicated-vs-serverless
