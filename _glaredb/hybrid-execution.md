---
layout: default
title: Hybrid Execution
nav_order: 3
---

# Hybrid execution

Connecting to a Cloud deployment through the [Python Library] or [CLI] enables
hybrid execution of SQL queries. With hybrid execution, queries utilize the
resources of both your local machine and the Cloud so that you can `SELECT` and
`JOIN` data across your Cloud deployment and your local file system.

Let's take a look at the following query:

```sql
select m.user_id,
  max(m.output_rows),
  avg(m.output_rows)::int
from execution_metrics m
  inner join './company_users.csv' u on m.user_id = u.id
group by m.user_id
limit 5;
```

In this example, `execution_metrics` is table that exists on the Cloud
deployment, and `./company_users.csv` is a CSV file that's sitting on your
laptop. With hybrid execution, the query gets executed across both your local
machine and Cloud deployment while minimizing the amount of data transferred
across machines.

## Getting started with hybrid execution

Hybrid execution requires a [Deployment] on GlareDB Cloud. Creating a deployment
is quick and easy.

Once you have a deployment ready to go, open the **Connect** dialog to get a set
of credentials for connecting to your deployment. This dialog provides the
commands needed to connect to your deployment using either the CLI or Python
library.

![Connect dialog]

Connecting via the CLI can be done with the `\open` command:

```text
> \open glaredb://user:password@hello.remote.glaredb.com:6443/hello
Connected to Cloud deployment: hello
```

And connecting via the Python library can be done with the `connect` method:

```python
import glaredb
con = glaredb.connect("glaredb://user:password@hello.remote.glaredb.com:6443/hello")
```

Once connected, you're able to query tables on your Cloud deployment, connected
data sources like [Postgres] and [Snowflake] databases, objects in S3, and files
on your local machine. All this without having to move data around.

## How it works

During query execution, GlareDB looks at where data referenced in the query is
located, and splits the query into separate pieces to be run on the remote node
and local machine. Some queries may be run entirely locally, or entirely remote
if it's determined if that's the most efficient way to run the query.

Let's take a look at some example queries.

A query that is only querying a local file will run entirely locally:

```sql
select * from './my_data.parquet';
```

A query that is only querying a table inside the database will run entirely on
the remote deployment (with the results being returned locally):

```sql
select * from my_table;
```

But joining across the table and local file will execute the query in fragments,
with parts of the query running locally, and parts running on the remote
deployment:

```sql
select * from my_table cross join './my_data.parquet';
```

This also applies to queries that are running with the Python library and
references a dataframe:

```python
import glaredb
import polars as pl

con = glaredb.connect("glaredb://user:password@hello.remote.glaredb.com:6443/hello")

polarsdf = pl.DataFrame({"fruits": ["banana", "banana", "apple", "apple", "banana"]})

# Note `my_cloud_table` is a table that exists in the Cloud deployment.
con.sql("select * from my_cloud_table cross join polarsdf").show()
```

Parts of queries that reference objects in S3/GCS or files over HTTP will be run
on the remote deployment:

```sql
-- Both queries will run entirely on the remote deployment.
select * from 'https://huggingface.co/datasets/fka/awesome-chatgpt-prompts/raw/main/prompts.csv';
select * from parquet_scan('s3://my_bucket/my_object.parquet', my_aws_creds);
```

### Queries referencing external data sources

What happens if join data from a connected data source like [Postgres] or
[Snowflake] with data from a local file?

During planning, the query gets split up such that the Cloud deployment is
responsible for pulling in the required data from the connected data source, and
the local machine is only responsible for execution the part of the query needed
to read the file. The local machine will never try to make a connection to the
external system.

[Postgres]: /docs/data-sources/supported/postgres.html
[Snowflake]: /docs/data-sources/supported/snowflake.html
[Deployment]: /cloud/deployments/
[Connect dialog]: /assets/images/glaredb/hybrid-execution/connect-dialog.png
[Python Library]: /glaredb/python/
[CLI]: /glaredb/local/
