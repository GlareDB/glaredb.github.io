---
title: Interoperability with Pandas and Polars
layout: default
nav_order: 2
parent: Tutorials
---

GlareDB can seamlessly read from, and write to, Panda and Polars. This enables
many interesting workflows for data exploration as well as integration with
other data tools.

## Select from a Pandas or Polars Dataframe with GlareDB

If you have a Pandas dataframe in memory, you can readily select from
it:

```python
import pandas as pd
import glaredb

df = pd.read_csv('https://github.com/GlareDB/glaredb/raw/main/testdata/csv/userdata1.csv')

con = glaredb.connect()
con.sql(
    """
        SELECT * FROM df WHERE country='Canada'
    """
).show()
```

The `df` variable, a Pandas dataframe, is included in the session scope and so
can be referenced in the GlareDB query as if it were a table in the database.

You can also do the same thing with a Polars dataframe:

```python
import polars as pl
import glaredb

polars_df = pl.read_csv('https://github.com/GlareDB/glaredb/raw/main/testdata/csv/userdata1.csv')

con = glaredb.connect()
con.sql(
    """
        SELECT * FROM polars_df WHERE country='Canada'
    """
).show()
```

## Assign the Results of a Query to a Dataframe

In addition to selecting from Pandas and Polars dataframes, GlareDB enables
yout to output the results of queries as Pandas and Polars dataframes:

```python
df = con.sql("SELECT 1").to_pandas()
polars_df = con.sql("SELECT 1").to_polars()
```

Putting it altogether, this lets you do things like construct a dataframe with
Pandas, manipulate it with SQL using GlareDB, and use the output again as a
dataframe:

```python
df = pd.read_csv('https://github.com/GlareDB/glaredb/raw/main/testdata/csv/userdata1.csv')

con = glaredb.connect()
canada_users = con.sql(
    """
        SELECT * FROM df WHERE country='Canada'
    """
).to_pandas()

canada_users_with_no_listed_professions = con.sql(
    """
        SELECT * FROM canada_users WHERE title IS NULL
    """
).to_pandas()
```

## Integration with Other Data Tools

Given the ease with which you can read from, and write to, Pandas and Polars
dataframes, and given how many other data tools can work with dataframes, this
can unlock some powerful workflows.

For instance, in [Dashboards Across Space and Time], you can learn how to
combine Streamlit with GlareDB data output as a dataframe to construct
complex dashboards with relatively little effort.

And in [Data Quality Across Space and Time], you can learn how to use Great
Expectations together with GlareDB data output as a dataframe to add data
quality checks to queries that you've run across databases.

[Dashboards Across Space and Time]: https://glaredb.com/blog/dashboards-across-space-and-time
[Data Quality Across Space and Time]: https://glaredb.com/blog/data-quality-across-space-and-time
