---
title: CLI
layout: default
nav_order: 4
parent: Installation
grand_parent: Introduction / Getting Started
---

# CLI

In addition to [Python] and [Node.js], GlareDB binaries are distributed through
[GitHub].

There are two ways to use GlareDB:

- **locally**, with optional disk persistence. In this scenario, queries are
  executed entirely in-process, and data exists in-memory or on-disk.

- **hybrid**, with [GlareDB Cloud]. In this scenario, queries are partitioned and
  optimized to run both in-process and using cloud compute. Data can be accessed
  and stored in cloud. When using [GlareDB Cloud], you can access your data
  in all of your applications.

## Install

The GlareDB binary can be installed through a simple script in the **current
directory**:

```shell
curl https://glaredb.com/install.sh | sh
```

Alternatively, you can download the appropriate binary from [GitHub].

The installation consists of just a single artifact, a binary called `glaredb`.
Application data is stored in `~/.glaredb`. Temporary files may be created in
standard locations like `/tmp` (for more information,
[see here](https://doc.rust-lang.org/std/env/fn.temp_dir.html)).

## Usage

The CLI can be used in scripts or interactively. It is very convenient for
small-scale ETL operations, local exploratory analysis and as a shell for
[GlareDB Cloud].

Each of these is covered below. To see the full list of options, run:

```shell
glaredb --help
```

### Local Exploratory Analysis

To start an interactive session, run `glaredb`. From here, SQL statements are
executed within a REPL, complete with syntax highlighting and support.

```shell
$ glaredb
Type \help for help.
>
```

Data sources (local and remote) can be analyzed and joined with ease:

```shell
>  SELECT * FROM './report.csv' r
::: JOIN read_excel('./my_workbook') e
::: ON r.name = e.name
::: WHERE r.output > 5;
```

### [GlareDB Cloud] shell

After signing up for [GlareDB Cloud], you can connect to your deployment from
the CLI either:

- by passing `--cloud-url` (`glaredb --cloud-url glaredb://user:pass@host:port/database`)
- or, if already in an interactive session, using `\open`:

```shell
$ glaredb
Type \help for help.
> \open glaredb://user:pass@host:port/database
```

Once a connection is opened to a cloud instance, all of its tables and data
can be accessed while also being able to access local files. Furthermore,
queries are optimized and partitioned to run using both local compute and 
cloud compute.

### Small-Scale ETL

`COPY TO` is a powerful feature that bridges the above use cases together. It
can be used to:

- Pull data from cloud, or other remote sources
- Interchange between data formats
- Push data from local to cloud or other remote sources

As an example, imagine you have a table in [GlareDB Cloud] called
`my_cloud_table`, and you want to perform some exploration on a subset of rows
in the table. The following query creates a local file `explore.csv` with the
desired rows.

```sql
COPY (
    SELECT * FROM my_cloud_table
    WHERE column_a > 10
    LIMIT 1000;
)
TO './explore.csv';
```

After analyzing and modifying the data, `COPY TO` can be used to save results
and even interchange the format (in this case, from CSV to Parquet):

```sql
COPY (SELECT * FROM './explore.csv') TO s3 FORMAT parquet OPTIONS (
  access_key_id = '<aws_access_key_id>',
  bucket = '<bucket>',
  location = 'explore.parquet',
  region = '<aws_region>',
  secret_access_key = '<aws_secret_access_key>'
);
```

<!-- TODO: Add Copy To doc link -->

Refer to the documentation for `COPY TO` for further specification and examples.

[Python]: /introduction/installation/python-bindings.html
[Node.js]: /introduction/installation/node_bindings.html
[GitHub]: https://github.com/GlareDB/glaredb/releases
[GlareDB Cloud]: https://console.glaredb.com
