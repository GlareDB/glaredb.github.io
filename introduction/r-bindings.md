---
title: R Bindings
layout: default
nav_order: 6
parent: Getting Started
---

TODO: Change example data to hosted file on github, and add example for local file too.

# R Bindings

GlareDB can be used in R environments along with [Pandas] and [Polars] to
work with distributed data thanks to the great work of [eitsupi].

## Install

The `glaredb` package can be installed from R-multiverse.

__Currently, Windows is not supported. Please use WSL2.__

To install the module:

```console
install.packages("glaredb", repos="https://community.r-multiverse.org")
```

## Usage

### Embedded Connection

Once installed, GlareDB can be used inside your R scripts by importing the
`glaredb` package, and creating a connection using `glaredb_connect`.

```r
library(glaredb)

con <- glaredb_connect()

glaredb_sql("SELECT 1", con) |> as_glaredb_table()
```


### Converting to a dataframe

In the above query, the results are formatted as a readable GlareDB table. It's
also possible to output your table as an R or Polars dataframe. Note: you will
also need to [install the Polars R bindings.]

```r
library(glaredb)
library(polars)

con <- glaredb_connect()

# Output as an R dataframe
r_dataframe <- glaredb_sql("SELECT 1", con) |> as.data.frame()

# Output as a Polars dataframe
polars_dataframe <- glaredb_sql("SELECT 1", con) |> as_polars_dataframe()
```

### Locally Persisted Data

By default, `connect` will use an in-memory database. To persist data locally,
a path may be provided to `connect`. Once you've created your connection
object, be sure to pass it into the call to `glaredb_sql`.

```r
library(glaredb)

con <- glaredb_connect("./my_db_path")
glaredb_sql("select * from persisted_table", con) |> as.data.frame()
```

### Cloud Connection

Provide a [connection string] to connect to [GlareDB Cloud].

```r
library(glaredb)

con <- glaredb_connect("glaredb://<user>:<password>@<org>.remote.glaredb.com:6443/<deployment-name>")
glaredb_sql("select * from cloud_table", con) |> as.data.frame()
```

Connecting to [GlareDB Cloud] with R enables [Hybrid execution]. Queries
are optimized to use both cloud and local compute resources.

### Querying data

GlareDB is able to query a variety of file types as tables directly.

TODO: Provide files for download

```r
library(glaredb)

con <- glaredb_connect()

# Query CSV files.
glaredb_sql("select * from './data.csv'", con) |> as.data.frame()

# Query JSON files.
glaredb_sql("select * from './data.json'", con) |> as.data.frame()

# Query Parquet files.
glaredb_sql("select * from './data.parquet'", con) |> as.data.frame()
```

Polars and Arrow dataframes can be queried as well. In the below examples,
Polars and Arrow dataframes are created, selected from with SQL using GlareDB,
and then output again to a native R dataframe.

```r
library(glaredb)

# Query a Polars dataframe
library(polars)

polars_df <- pl$DataFrame(
  A = 1:5,
  fruits = c("banana", "banana", "apple", "apple", "banana"),
  B = 5:1,
  C = c("beetle", "audi", "beetle", "beetle", "beetle")
)

result <- glaredb_sql("select * from polars_df where fruits = 'banana'") |>
  as.data.frame()

result

# Query an Arrow dataframe
library(arrow)

arrow_df <- data.frame(
  A = 1:5,
  fruits = c("banana", "banana", "apple", "apple", "banana"),
  B = 5:1,
  C = c("beetle", "audi", "beetle", "beetle", "beetle")
) |> arrow_table()

result <- glaredb_sql("select * from arrow_df where fruits = 'banana'") |> 
  as.data.frame()
```

As with files, GlareDB can access these dataframes directly once they
are variables in the scope of your Python environment.

Note: Native R dataframes cannot be selected from in this way, since they are
not based on the Apache Arrow format. If you would like to select from a native
R dataframe directly with GlareDB, you must first coerce it to Polars or 
Arrow.

### Lazy evaluation
TODO: COnfirm
The `sql` method returns the logical plan of the query passed in as an
argument. This means that the query is not executed until one of the dataframe
conversion methods, like `as_glaredb_table()`, `as.data.frame()`, or 
`as_polars_dataframe()` are called.

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

TODO: Uppercase all of the SQL statements
Eagerly evaulating a query can be done via the `glaredb_execute` method. This will
execute the provided query to completion. This is useful when the result of a
query doesn't matter (e.g. when creating a table, inserting data into a
table, or other DDL operations).

```r
library(glaredb)

con <- glaredb_connect("./my_db_path")

# Create a table.
glaredb_execute("create table my_table (a int)", con)

# Insert some data.
glaredb_execute("insert into my_table values (1), (2)", con)

glaredb_sql("select * from my_table", con) |> as.data.frame()

# ┌───────┐
# │ a     │
# │ ──    │
# │ Int32 │
# ╞═══════╡
# │ 1     │
# │ 2     │
# └───────┘
```

## Example

{: .important}

> For more examples, see <https://github.com/GlareDB/glaredb/tree/main/py-glaredb/examples>

The following is an example that joins a polars data frame with data from a
hosted demo Postgres instance.

```r
library(glaredb)
library(polars)

# Create Polars DataFrame 
polars_df <- pl$DataFrame(
  region = c(0, 1, 2, 3, 4),
  population = c(10, 20, 30, 40, 50)
)

con <- glaredb_connect()

# Join the above Polars DataFrame on data from our demo Postgres instance
# Note: This uses a heredoc-style string in R (available in R >0.4.0) to make
# it possible to write the SQL statement on multiple lines. 

result <- glaredb_sql(R"(
        select
            t1.r_regionkey,
            t1.r_name,
            t2.Population
        from
            read_postgres('postgres://demo:demo@pg.demo.glaredb.com/postgres', 'public', 'region') as t1
        join
            polars_df as t2 on t1.r_regionkey = t2.region;)", con
) |> as_polars_dataframe()
result
```

The above results in:

```console
shape: (5, 3)
┌─────────────┬───────────────────────────┬────────────┐
│ r_regionkey ┆ r_name                    ┆ population │
│ ---         ┆ ---                       ┆ ---        │
│ i32         ┆ str                       ┆ f64        │
╞═════════════╪═══════════════════════════╪════════════╡
│ 0           ┆ AFRICA                    ┆ 10.0       │
│ 2           ┆ ASIA                      ┆ 30.0       │
│ 1           ┆ AMERICA                   ┆ 20.0       │
│ 4           ┆ MIDDLE EAST               ┆ 50.0       │
│ 3           ┆ EUROPE                    ┆ 40.0       │
└─────────────┴───────────────────────────┴────────────┘
```

[Pandas]: https://github.com/pandas-dev/pandas
[Polars]: https://github.com/pola-rs/polars
[install the Polars R bindings.]: https://github.com/pola-rs/r-polars
[blog post Working with Python]: https://glaredb.com/blog/working-with-python
[GlareDB Cloud]: https://console.glaredb.com
[connection string]: /glaredb/hybrid-execution/#getting-started-with-hybrid-execution
[Hybrid execution]: /glaredb/hybrid-execution
