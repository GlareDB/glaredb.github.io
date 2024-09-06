---
title: R Bindings
layout: default
nav_order: 6
parent: Getting Started
---

# R Bindings

GlareDB can be used in R environments along with [Pandas] and [Polars] to
work with distributed data thanks to [eitsupi's great contribution].

## Install

The `glaredb` package can be installed from R-multiverse.

**Currently, Windows is not supported. Please use WSL2.**

To install the module:

```console
sys.setenv(NOT_CRAN = "true")
install.packages("glaredb", repos = c("https://community.r-multiverse.org", options("repos")))
```

## Usage

### Embedded Connection

Once installed, GlareDB can be used inside your R scripts by importing the
`glaredb` package, and creating a connection using `glaredb_connect`.

```r
library(glaredb)

con <- glaredb_connect()

# Select from a remote Parquet file hosted on GitHub
glaredb_sql(
    "SELECT * FROM 'https://github.com/GlareDB/glaredb/raw/main/testdata/parquet/userdata1.parquet'",
    con
    ) |> as_glaredb_table()
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
r_dataframe <- glaredb_sql(
    "SELECT * FROM 'https://github.com/GlareDB/glaredb/raw/main/testdata/parquet/userdata1.parquet'",
    con
) |> as.data.frame()

# Output as a Polars dataframe
polars_dataframe <- glaredb_sql(
    "SELECT * FROM 'https://github.com/GlareDB/glaredb/raw/main/testdata/parquet/userdata1.parquet'",
    con
) |> as_polars_dataframe()
```

### Locally Persisted Data

By default, `connect` will use an in-memory database. To persist data locally,
a path may be provided to `connect`. Once you've created your connection
object, be sure to pass it into the call to `glaredb_sql`.

```r
library(glaredb)

con <- glaredb_connect("./my_db_path")
glaredb_execute("CREATE TABLE my_table AS SELECT 1", con)

# After closing your session, you can re-open a connection to the same directory
con <- glaredb_connect("./my_db_path")
glaredb_sql("SELECT * FROM my_table", con) |> as.data.frame()
```

### Cloud Connection

Provide a [connection string] to connect to [GlareDB Cloud].

```r
library(glaredb)

con <- glaredb_connect("glaredb://<user>:<password>@<org>.remote.glaredb.com:6443/<deployment-name>")
glaredb_sql("SELECT * FROM previously_created_cloud_table", con) |> as.data.frame()
```

In addition to a shared workspace with data that is accessible to multiple
users, connecting to [GlareDB Cloud] with R enables [Hybrid execution]. Queries
are optimized to use both cloud and local compute resources.

### Querying Data

#### Querying Files

GlareDB is able to query a variety of file types as tables directly.

You can download sample data for the following examples here:

- [CSV]
- [JSON]
- [Parquet]

You can also query the raw files hosted on GitHub directly [as shown above].

```r
library(glaredb)

con <- glaredb_connect()

# Query CSV files.
glaredb_sql("SELECT * FROM './userdata1.csv'", con) |> as.data.frame()

# Query JSON files.
glaredb_sql("SELECT * FROM './userdata1.json'", con) |> as.data.frame()

# Query Parquet files.
glaredb_sql("SELECT * FROM './userdata1.parquet'", con) |> as.data.frame()

# Absolute file paths work also
glaredb_sql("SELECT * FROM 'Users/my_user/Downloads/userdata1.json'", con) |> as.data.frame()

```

#### Querying In-Memory Data

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

result <- glaredb_sql("SELECT * FROM polars_df where fruits = 'banana'") |>
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

result <- glaredb_sql("SELECT * FROM arrow_df where fruits = 'banana'") |>
  as.data.frame()
```

As with files, GlareDB can access these dataframes directly once they
are variables in the scope of your R environment.

Note: Native R dataframes cannot be selected from in this way, since they are
not based on the Apache Arrow format. If you would like to select from a native
R dataframe directly with GlareDB, you must first coerce it to Polars or
Arrow.

### Lazy evaluation

The `glaredb_sql` method returns the logical plan of the query passed in as an
argument. This means that the query is not executed until one of the dataframe
conversion methods, like `as_glaredb_table()`, `as.data.frame()`, or
`as_polars_dataframe()` are called.

This can be used to incrementally build up sql queries by referencing previously
defined logical plans created with `glaredb_sql`.

```r
library(glaredb)

con <- glaredb_connect()

# Note: This uses a heredoc-style string in R (available in R >0.4.0) to make
# it possible to write the SQL statement on multiple lines.
intermediate <- glaredb_sql(R"(
    SELECT
        *
    FROM
        'https://github.com/GlareDB/glaredb/raw/main/testdata/parquet/userdata1.parquet'
    )",
    con
)

result <- glaredb_sql(R"(
    SELECT
        first_name,
        last_name,
        birthdate
    FROM
        intermediate
    WHERE
        country = 'Canada'
    LIMIT 5
    )",
    con
) |> as.data.frame()

result
```

```console
  first_name last_name birthdate
1     Albert   Freeman 1/16/1968
2    Deborah Armstrong  4/8/1969
3     Gloria  Hamilton  3/9/1988
4      Aaron    Torres 4/18/1980
5      Peter   Russell 9/26/1976
```

### Eager evalutation

Eagerly evaulating a query can be done via the `glaredb_execute` method. This will
execute the provided query to completion. This is useful when the result of a
query doesn't matter (e.g. when creating a table, inserting data into a
table, or other DDL operations).

```r
library(glaredb)

con <- glaredb_connect("./my_db_path")

# Create a table.
glaredb_execute("CREATE TABLE my_table (a INT)", con)

# Insert some data.
glaredb_execute("INSERT INTO my_table VALUES (1), (2)", con)

glaredb_sql("SELECT * FROM my_table", con) |> as.data.frame()
```

```console
  a
1 1
2 2
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

result <- glaredb_sql(R"(
        SELECT
            t1.r_regionkey,
            t1.r_name,
            t2.Population
        FROM
            read_postgres('postgres://demo:demo@pg.demo.glaredb.com/postgres', 'public', 'region') t1
        JOIN
            polars_df t2
        ON t1.r_regionkey = t2.region;)", con
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

[eitsupi's great contribution]: https://github.com/eitsupi/r-glaredb
[Pandas]: https://github.com/pandas-dev/pandas
[Polars]: https://github.com/pola-rs/polars
[install the Polars R bindings.]: https://github.com/pola-rs/r-polars
[CSV]: https://github.com/GlareDB/glaredb/raw/main/testdata/csv/userdata1.csv
[JSON]: https://github.com/GlareDB/glaredb/raw/main/testdata/json/userdata1.json
[Parquet]: https://github.com/GlareDB/glaredb/raw/main/testdata/parquet/userdata1.parquet
[as shown above]: #embedded-connection
[GlareDB Cloud]: https://console.glaredb.com
[connection string]: /glaredb/hybrid-execution/#getting-started-with-hybrid-execution
[Hybrid execution]: /glaredb/hybrid-execution
