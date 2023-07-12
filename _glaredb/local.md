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

{: .important}

> Running `glaredb` locally is an in-memory process. Once the program exits, all
> data will be lost.

To start a local session, run:

```console
./glaredb local
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
