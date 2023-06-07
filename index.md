---
title: What is GlareDB?
layout: home
nav_order: 1
has_children: true
---

# What is GlareDB?

GlareDB is a database built for querying and analyzing distributed data using
SQL. Query data directly from [Postgres], [Snowflake], [object storage],
[and other data sources] without moving data around.

## GlareDB & GlareDB Cloud

{: .important}

> GlareDB and GlareDB Cloud are in [Technical Preview].

GlareDB is open source and is freely available to install and use. Get started
at [github.com/GlareDB/glaredb].

GlareDB Cloud is a fully managed offering of GlareDB with additional features
for access management and compute resources. GlareDB Cloud is generally
available to everyone with a free tier. Get started at [console.glaredb.com].

## What is a data source?

A data source is a destination with data, such as databases or files.

We currently support multiple databases and files in [object storage]. For
example, you can join data existing in a [Postgres] database with a CSV in [S3]
using basic SQL. There is no need for ETL!

[Learn more about data sources].

## Where does GlareDB fit into your stack?

GlareDB sits between your data applications and your data sources. Any
application or client that can communicate using the Postgres protocol can
connect directly to GlareDB.

![Where GlareDB fits](/assets/images/where-glaredb-fits.png)

## Fully managed

Whether you use our serverless (free) or dedicated (paid plan) databases,
GlareDB Cloud is fully managed. With a few clicks, a GlareDB deployment will be
ready and highly available for you to use.

[Learn more about serverless and dedicated]

[Postgres]: /cloud/data-sources/supported/postgres/
[Snowflake]: /cloud/data-sources/supported/snowflake/
[object storage]: /cloud/data-sources/supported/gcs/
[and other data sources]: /cloud/data-sources/supported/index/
[Technical Preview]: /docs/about/technical-preview.html
[github.com/GlareDB/glaredb]: https://github.com/GlareDB/glaredb
[console.glaredb.com]: https://console.glaredb.com
[S3]: /cloud/data-sources/supported/s3/
[Learn more about data sources]: /docs/data-sources/
[Learn more about serverless and dedicated]: /cloud/deployments.html#dedicated-vs-serverless
