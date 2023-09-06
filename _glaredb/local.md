---
layout: default
title: GlareDB CLI
nav_order: 1
---

# GlareDB CLI

## Install

GlareDB can be installed in the **current working directory** with a simple one-line
command:

```console
curl https://glaredb.com/install.sh | sh
```

## Update

To update GlareDB, simply re-run the [Install](#install). The install works in
the current working directory and will **replace/overwrite existing installations**.

## Basic usage

To start a local session, run:

```sh
./glaredb
```

This will drop you into a shell letting you run sql commands against GlareDB.
Note that by default, this will use an in-memory database.

```text
GlareDB
Type \help for help.
Using in-memory catalog
> select 'hello glaredb';
┌───────────────────────┐
│ Utf8("hello glaredb") │
│ ──                    │
│ Utf8                  │
╞═══════════════════════╡
│ hello glaredb         │
└───────────────────────┘
```

An optional `--data-dir` argument can be provided which will persist the
database at the provided path.

```sh
./glaredb --data-dir ./example
```

The `\open` command can be used in a running shell to open a database at the
provided path:

```text
> \open ./example
```

The `\open` command can also be used to connect to a GlareDB Cloud deployment.

```text
> \open glaredb://<user>:<password>@<org>.remote.glaredb.com:6443/<deployment-name>
Connected to Cloud deployment: <deployment-name>
```

Connecting to a Cloud deployment via the CLI enables [Hybrid execution] which
allows queries to use the resources of both the remote deployment and local
machine.

## Server usage

Alternatively, the server subcommand can be used to launch a server process on
port `6543`:

```sh
./glaredb server
```

To see all options available, run `--help`:

```sh
./glaredb server --help
```

The server can then be connected with a Postgres-compatible client, for example
`psql`:

```sh
psql "host=localhost user=glaredb dbname=glaredb port=6543"
```

### Connecting to a local server with other programming languages

You can connect to a GlareDB server running locally (or remotely) with your
programming language of choice.

The [GlareDB Repository] has the following examples:

- [R]
- [go]
- [Node.js]

## Using GlareDB's python bindings

GlareDB has specific bindings for Python that allow for interop with data
processing libraries like [Polars] and [Pandas]. For more information, see the
following:

- [Our Python Bindings documentation]
- [Our blog post on Python Bindings]
- [Our examples on using GlareDB in Python]

[Hybrid execution]: /glaredb/hybrid-execution
[Pandas]: https://github.com/pandas-dev/pandas
[Polars]: https://github.com/pola-rs/polars
[Our Python Bindings documentation]: /glaredb/python/
[Our blog post on Python Bindings]: https://glaredb.com/blog/working-with-python
[Our examples on using GlareDB in Python]: https://github.com/GlareDB/glaredb/tree/main/py-glaredb/examples
[GlareDB Repository]: https://github.com/GlareDB/glaredb
[R]: https://github.com/GlareDB/glaredb/tree/main/examples/R
[go]: https://github.com/GlareDB/glaredb/tree/main/examples/go
[Node.js]: https://github.com/GlareDB/glaredb/tree/main/examples/typescript
