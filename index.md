---
title: What is GlareDB?
layout: home
nav_order: 1
has_children: true
---

## What is GlareDB?

Data lives everywhere, as files on laptops, servers, and [S3], or in
other database systems like [Postgres], [Snowflake], and
[MongoDB]. Data lives in many formats, like [Excel], [CSV] and
[Parquet]. And this is just the beginning. *GlareDB is a tool that
recognizes that it makes sense to store and work with data in
different systems*, and provides a system for querying, manipulating,
and storing data in the best way possible.

**GlareDB makes all of your data SQL addressable, no matter what form
it's in** So you can query (and `JOIN`!) and manipulate your data it
using standard tools that you may already know.

## How do I get it?

If you're working with data from Python or Node.js, you can get a
complete GlareDB with just:

```shell
pip install glaredb
```

or:

```shell
npm install glaredb
```

You can install an interactive terminal program `glaredb` with:

```shell
curl https://glaredb.com/install.sh | sh
```

You can sign up for [GlareDB Cloud], which provides fully managed and
entirely severless deployments via the PostgreSQL protocol.

Don't worry! If you start using the embedded version of GlareDB and
later out grow the confines of your laptop (or edge function!) moving
to GlareDB Cloud just requires adding a connection string!

See the [Getting started] guide for more!

## Where does GlareDB fit into your stack?

![Where GlareDB fits](/assets/images/where-glaredb-fits.png)

Where ever you need it too! GlareDB brings a complete, fully featured
data analytics engine to wherever you're working with data. Use glare
do be:

- query local Excel and CSV files and join them with remote Parquet
  and JSON files.

- join tables from PostgreSQL and Snowflake, with data from MongoDB
  collections.

- write the output of any query to GlareDB-native storage for quick
  and easy access letter.

- copy data between MongoDB and Postgres to Snowflake or GlareDB-native
  storage.

- pass data from your data sources to DataFrame libraries in Python
  like Pandas and Polars.

- explore data from the command line or your favorite notebook.

See the [Working with GlareDB in Python] blog post and [Examples page]
for more examples.

### What is a Data Source?

A data source is something that you can query in GlareDB: local files,
database system, files in blob storage like [S3] or [GCS], sometimes
it's an arbitrary HTTP endpoint.

[Learn more about data sources].

## Offerings

**GlareDB** is open source and is freely available to install and use. Get
started at [github.com/GlareDB/glaredb].

You can run GlareDB locally and in Python.

- [Learn more about `glaredb local`]
- [Learn more about Python bindings]
- [Learn more about Node.js bindings]

**GlareDB Cloud** is a fully managed serverless GlareDB service. In
addition to everything from the core GlareDB engine, it provides
additional features for access management and compute resources that
scale with your use. There's *no* cold-start and no resource
allocation. GlareDB Cloud is available to everyone with a
[free tier]. Get started at [console.glaredb.com].

See our [Pricing page] for more details on available plans.

[Postgres]: /docs/data-sources/supported/postgres/
[Snowflake]: /docs/data-sources/supported/snowflake/
[S3]: /docs/data-sources/supported/s3/
[Getting started]: /docs/about/getting-started
[Examples page]: /glaredb/examples/index/
[Working with GlareDB in Python]: https://glaredb.com/blog/working-with-python
[GCS]: /docs/data-sources/supported/gcs/
[Learn more about data sources]: /docs/data-sources/
[github.com/GlareDB/glaredb]: https://github.com/GlareDB/glaredb#install
[Learn more about `glaredb local`]: /glaredb/local
[Learn more about Python bindings]: /glaredb/python
[Learn more about Node.js bindings]: /glaredb/node
[free tier]: /docs/about/free-tier.html
[Pricing page]: https://glaredb.com/pricing
[console.glaredb.com]: https://console.glaredb.com
