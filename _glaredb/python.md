---
layout: default
title: GlareDB Python library
nav_order: 2
---

# GlareDB Python library

GlareDB can be used in Python environments along with [Pandas] and [Polars] to
work with distributed data.

For more information, refer to our in-depth [blog post Working with Python].

## Install

The `glaredb` module is available on PyPI <https://pypi.org/project/glaredb/>.
To install the module:

```console
pip install glaredb
```

## Usage

Once installed, GlareDB can be used inside your python scripts by importing the
`glaredb` library, and creating a connection using `connect`.

```python
import glaredb

con = glaredb.connect()
con.sql("select 1").show()
```

By default, `connect` will use an in-memory database. A path may be provided to
`connect` to persist data after the python script exits.

```python
import glaredb

con = glaredb.connect("./my_db_path")
con.sql("select * from persisted_table").show()
```

Provide a [connection string] to connect to [GlareDB Cloud].

```python
import glaredb

con = glaredb.connect("glaredb://<user>:<password>@<org>.remote.glaredb.com:6443/<deployment-name>")
con.sql("select * from cloud_table").show()
```

Connecting to [GlareDB Cloud] with Python enables [Hybrid execution]. Queries
are optimized to use cloud and local compute resources. 

### Querying data

GlareDB is able to query a variety of file types directly from the python library.

```python
import glaredb
con = glaredb.connect()

# Query CSV files.
con.sql("select * from './data.csv'").show()

# Query JSON files.
con.sql("select * from './data.json'").show()

# Query Parquet files.
con.sql("select * from './data.parquet'").show()
```

Polars and Pandas dataframes can be queried as well.

```python
import glaredb
con = glaredb.connect()

# Query a Pandas dataframe
import pandas as pd
pandasdf = pd.DataFrame({"fruits": ["banana", "banana", "apple", "apple", "banana"]})
con.sql("select * from pandasdf")

# Query a Polars dataframe
import polars as pl
polarsdf = pl.DataFrame({"fruits": ["banana", "banana", "apple", "apple", "banana"]})
con.sql("select * from polarsdf")
```

### Converting to a dataframe

The GlareDB connection allows converting results into Polars or Pandas dataframes.

```python
import glaredb
con = glaredb.connect()

# Convert to a Pandas dataframe
pandas_out = con.sql("select 1").to_pandas()

# Convert to a Polars dataframe
polars_out = con.sql("select 1").to_polars()
```

### Lazy evaluation

The `sql` method returns logical plan of the query passed in as an argument.
What this means is the query is not executed until `show` or one of the
dataframe conversion methods (`to_pandas`, etc) are called.

This can be used to incrementally build up sql queries by referencing previously
defined logical plans created with `sql`.

```python
import glaredb
import pandas as pd

con = glaredb.connect()

df = pd.DataFrame(
    {
        "a": [1, 2, 3, 4, 5],
        "fruits": ["banana", "banana", "apple", "apple", "banana"],
        "b": [5, 4, 3, 2, 1],
        "cars": ["beetle", "audi", "beetle", "beetle", "beetle"],
    }
)


intermediate = con.sql("select * from df where a > 2;")

# Note that we reference the variable 'intermediate' here.
con.sql("select * from intermediate where fruits = 'apple';").show()

# ┌───────┬────────┬───────┬────────┐
# │ a     │ fruits │ b     │ cars   │
# │ ──    │ ──     │ ──    │ ──     │
# │ Int64 │ Utf8   │ Int64 │ Utf8   │
# ╞═══════╪════════╪═══════╪════════╡
# │ 3     │ apple  │ 3     │ beetle │
# │ 4     │ apple  │ 2     │ beetle │
# └───────┴────────┴───────┴────────┘
```

### Eager evalutation

Eagerly evaulating a query can be done via the `execute` method. This will
execute the provided query to completion. This is useful when the result of a
query doesn't matter (e.g. when creating a table or inserting data into a
table).

```python
import glaredb
con = glaredb.connect()

# Create a table.
con.execute("create table my_table (a int)")
# Insert some data.
con.execute("insert into my_table values (1), (2)")

# Query the table we just created. Note that we're using `sql` here because we
# want to show the results.
con.sql("select * from my_table").show()

# ┌───────┐
# │ a     │
# │ ──    │
# │ Int32 │
# ╞═══════╡
# │ 1     │
# │ 2     │
# └───────┘
```

## API

- `module glaredb`
  - `connect([data_dir], [spill_path]): LocalSession`
    - `data_dir` optional - if provided, data will be stored at this path,
      otherwise all data is in memory.
    - `spill_path` optional - a path where glaredb can create temporary files.
      If not provided, a random temporary directory is used.
- `class LocalSession`
  - `prql(query): PyLogicalPlan`
    - Lazily evaluates the `query` string (PRQL syntax)
  - `sql(query): PyLogicalPlan`
    - Lazily evaluates the `query` string (SQL syntax)
  - `execute(query): PyExecutionResult`
    - Eagerly evaluates the `query` string (SQL syntax)
  - `close()`
- `class PyLogicalPlan`
  - `to_arrow()`
  - `to_pandas()`
  - `to_polars()`
  - `show()`
- `class PyExecutionResult`
  - `to_arrow()`
  - `to_pandas()`
  - `to_polars()`
  - `show()`

## Example

{: .important}

> For more examples, see <https://github.com/GlareDB/glaredb/tree/main/py-glaredb/examples>

The following is an example that joins a polars data frame with data from a demo
Postgres instance that we host.

```python
import glaredb
import polars as pl

# Polars DataFrame created in the script
df = pl.DataFrame(
    {
        "region": [0, 1, 2, 3, 4],
        "population": [10, 20, 30, 40, 50]
    }
)

con = glaredb.connect()

# Join the above Polars DataFrame on data from our demo Postgres instance
result = con.sql(
        """select
            t1.r_regionkey,
            t1.r_name,
            t2.Population
        from
            read_postgres('postgres://demo:demo@pg.demo.glaredb.com/postgres', 'public', 'region') as t1
        join
            df as t2 on t1.r_regionkey = t2.region;"""
).to_polars();

print(result)
```

The above results in:

```console
shape: (5, 3)
┌─────────────┬───────────────────────────┬────────────┐
│ r_regionkey ┆ r_name                    ┆ population │
│ ---         ┆ ---                       ┆ ---        │
│ i32         ┆ str                       ┆ i64        │
╞═════════════╪═══════════════════════════╪════════════╡
│ 3           ┆ EUROPE                    ┆ 40         │
│ 0           ┆ AFRICA                    ┆ 10         │
│ 2           ┆ ASIA                      ┆ 30         │
│ 4           ┆ MIDDLE EAST               ┆ 50         │
│ 1           ┆ AMERICA                   ┆ 20         │
└─────────────┴───────────────────────────┴────────────┘
```

[Pandas]: https://github.com/pandas-dev/pandas
[Polars]: https://github.com/pola-rs/polars
[blog post Working with Python]: https://glaredb.com/blog/working-with-python
[GlareDB Cloud]: https://console.glaredb.com
[connection string]: /glaredb/hybrid-execution/#getting-started-with-hybrid-execution
[Hybrid execution]: /glaredb/hybrid-execution
