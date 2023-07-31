---
layout: default
title: Local
nav_order: 1
---

# Try GlareDB locally

## Install

GlareDB can be installed in the current working directory with a simple one-line
command:

```console
curl https://glaredb.com/install.sh | sh
```

## Running

To start a local session, run:

```sh
./glaredb local
# You can use `--data-dir` to specify a disk-backed data directory:
./glaredb local --data-dir /tmp/glaredb
# See `./glaredb local --help` for more options.
```

Alternatively, the server subcommand can be used to launch a server process on
port `6543`:

```console
./glaredb server
```

The server can then be connected with a Postgres-compatible client, for example
`psql`:

```console
psql "host=localhost user=glaredb dbname=glaredb port=6543"
```
