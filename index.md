---
title: What is GlareDB?
layout: home
nav_order: 1
has_children: true
---

# What is GlareDB?

Data exists everywhere: your laptop, [Postgres], [Snowflake] and as
[files in GCS]. It exists in various formats such as Parquet, CSV and JSON.
Regardless, there will always be multiple steps spanning several destinations to
get the insights you need.

**GlareDB is designed to query your data wherever it lives using SQL that you
already know.**

[Getting started] is as easy as:

```shell
curl https://glaredb.com/install.sh | sh
```

## Where does GlareDB fit into your stack?

![Where GlareDB fits](/assets/images/where-glaredb-fits.png)

GlareDB is versatile in that it can:

- query local and remote files
- query other databases and data sources
- store data and queries (as views)
- copy data from sources to destinations
- interop with DataFrame libraries in Python
- run one-off queries from the command-line

See our [Working with GlareDB in Python] blog post and our [Examples page] for
in-depth examples.

### What is a data source?

A data source is a destination with data, such as databases or files.

We currently support various databases and files in [GCS] and [S3].

[Learn more about data sources].

## Offerings

**GlareDB** is open source and is freely available to install and use. Get started
at [github.com/GlareDB/glaredb]. See our [open source announcement] for more information.

You can run GlareDB locally or even within Python.

- [Learn more about `glaredb local`]
- [Learn more about Python bindings]

**GlareDB Cloud** is a fully managed offering of GlareDB with additional features
for access management and compute resources. GlareDB Cloud is generally
available to everyone with a [free tier]. Get started at [console.glaredb.com].

## Fully managed

Whether you use our serverless compute (free) or create dedicated compute engines
(paid plan), GlareDB Cloud is fully managed. With a few clicks, a GlareDB deployment
will be ready and highly available for you to use.

[Learn more about serverless and dedicated]

[Postgres]: /docs/data-sources/supported/postgres/
[Snowflake]: /docs/data-sources/supported/snowflake/
[files in GCS]: /docs/data-sources/supported/gcs/
[Getting started]: /docs/about/getting-started
[Examples page]: /glaredb/examples/index/
[Working with GlareDB in Python]: https://glaredb.com/blog/working-with-python
[GCS]: /docs/data-sources/supported/gcs/
[S3]: /docs/data-sources/supported/s3/
[Learn more about data sources]: /docs/data-sources/
[github.com/GlareDB/glaredb]: https://github.com/GlareDB/glaredb#install
[Learn more about `glaredb local`]: /glaredb/local
[Learn more about Python bindings]: /glaredb/python
[free tier]: /docs/about/free-tier.html
[console.glaredb.com]: https://console.glaredb.com
[Learn more about serverless and dedicated]: /cloud/deployments/#dedicated-vs-serverless
