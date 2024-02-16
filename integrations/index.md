---
title: Integrations
layout: home
nav_order: 4
has_children: true
---

# Supported integrations

GlareDB and GlareDB Cloud can be used with a wide range of other data tools
using both Postgres protocols and GlareDB's interoperability with Pandas and
Polars DataFrames.

## Postgres protocols

GlareDB lets you connect using a Postgres connection string, which means that
data tools that can connect to Postgres *may just work* with GlareDB.

### GlareDB Cloud

If you click the Connect button in Cloud, you will see a window which shows a few
possibilities for connection strings. Select Postgres to get a connection string
that you can use to connect.

### GlareDB local

Using GlareDB locally? You can spin up GlareDB as a local Postgres server using

```shell
./glaredb server --data-dir <path to your GlareDB instance>
```

Then you can connect using

```shell
postgresql://test:test@localhost:6543/default
```

(The username and password don't matter.)

## Bugs

If you find a bug when connecting GlareDB with another data tool,
[please let us know]! We are always working to improve the quality
and test coverage of integrations with GlareDB.

[please let us know]: https://github.com/GlareDB/glaredb/issues/new?assignees=&labels=bug+%3Abug%3A&projects=&template=bug-report.md&title=
