---
layout: default
title: Python bindings
nav_order: 2
---

# Use GlareDB with Python

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

{: .important}

> GlareDB is run as a local process in Python environments. Connections to remote
> instances of GlareDB will be supported in a future version.

- import the `glaredb` module
- `connect` and then either `execute` eagerly or lazily with `sql`

### Intermediates

Using `.sql` to lazily evaluate let's you store a logical plan in a variable so
that you can incrementally build up queries.

```python
intermediate = con.sql("select * from tbl where a > 2;")

# note that we reference the variable 'intermediate' here
con.sql("select * from intermediate where b > 4;")
```

### API

- `module glaredb`
  - `connect([data_dir], [spill_path]): LocalSession`
    - `data_dir` optional - if provided, data will be stored at this path,
      otherwise all data is in memory.
    - `spill_path` optional - a path where glaredb can create temporary files.
      If not provided, a random temporary directory is used.
- `class LocalSession`
  - `sql(query): PyLogicalPlan`
    - Lazily evaluates the `query` string
  - `execute(query): PyExecutionResult`
    - Eagerly evaluates the `query` string
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
