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

As of June 2023, GlareDB is open source! See our [open source announcement] for
more information.

## Where does GlareDB fit into your stack?

GlareDB sits between your data applications and your data sources. Any
application or client that can communicate using the Postgres protocol can
connect directly to GlareDB.

![Where GlareDB fits](/assets/images/where-glaredb-fits.png)

## What is a data source?

A data source is a destination with data, such as databases or files.

We currently support multiple databases and files in [object storage]. For
example, you can join data existing in a [Postgres] database with a CSV in [S3]
using basic SQL. There is no need for ETL!

[Learn more about data sources].

## Offerings

**GlareDB** is open source and is freely available to install and use. Get started
at [github.com/GlareDB/glaredb]. See our [open source announcement] for more information.

**GlareDB Cloud** is a fully managed offering of GlareDB with additional features
for access management and compute resources. GlareDB Cloud is generally
available to everyone with a [free tier]. Get started at [console.glaredb.com].

## Fully managed

Whether you use our serverless (free) or dedicated (paid plan) databases,
GlareDB Cloud is fully managed. With a few clicks, a GlareDB deployment will be
ready and highly available for you to use.

[Learn more about serverless and dedicated]

[Postgres]: /docs/data-sources/supported/postgres/
[Snowflake]: /docs/data-sources/supported/snowflake/
[object storage]: /docs/data-sources/supported/gcs/
[and other data sources]: /docs/data-sources/supported/index/
[S3]: /docs/data-sources/supported/s3/
[Learn more about data sources]: /docs/data-sources/
[github.com/GlareDB/glaredb]: https://github.com/GlareDB/glaredb#install
[open source announcement]: https://glaredb.com/blog/glaredb-goes-open-source
[free tier]: /docs/about/free-tier.html
[console.glaredb.com]: https://console.glaredb.com
[Learn more about serverless and dedicated]: /cloud/deployments/#dedicated-vs-serverless
