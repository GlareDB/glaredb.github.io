---
layout: default
title: Run GlareDB locally
nav_order: 1
---

# Run GlareDB locally

## Install

GlareDB can be installed in the **current working directory** with a simple one-line
command:

```console
curl https://glaredb.com/install.sh | sh
```

## Update

To update GlareDB, simply re-run the [Install](#install). The install works in
the current working directory and will **replace/overwrite existing installations**.

## Running

To start a local session, run:

```sh
./glaredb
```

To see all options available, run `--help`:

```sh
./glaredb --help
```

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

## Connecting to a local server with Python

GlareDB has specific bindings for Python that allow for interop with data
processing libraries like [Polars] and [Pandas]. For more information, see the
following:

- [Our Python Bindings documentation]
- [Our blog post on Python Bindings]
- [Our examples on using GlareDB in Python]

## Connecting to a local server with other programming languages

You can connect to a GlareDB server running locally (or remotely) with your
programming language of choice.

The [GlareDB Repository] has the following examples:

- [R]
- [go]
- [Node.js]

[Pandas]: https://github.com/pandas-dev/pandas
[Polars]: https://github.com/pola-rs/polars
[Our Python Bindings documentation]: /glaredb/python/
[Our blog post on Python Bindings]: https://glaredb.com/blog/working-with-python
[Our examples on using GlareDB in Python]: https://github.com/GlareDB/glaredb/tree/main/py-glaredb/examples
[GlareDB Repository]: https://github.com/GlareDB/glaredb
[R]: https://github.com/GlareDB/glaredb/tree/main/examples/R
[go]: https://github.com/GlareDB/glaredb/tree/main/examples/go
[Node.js]: https://github.com/GlareDB/glaredb/tree/main/examples/typescript
