---
layout: default
title: System catalog
has_children: true
---

# System catalog

This topic provides an overview of builtin objects, how they relate, and how
they can be queried.

## The `default` database

Every GlareDB deployment is initialized with a `default` database. This database
cannot be dropped. Schemas, views, and external tables can be created within
this database.

The `default` database contains three schemas providing information about a
running system.

- `glare_catalog`: A schema containing internal information about the
  deployment.
- `pg_catalog`: A set of views on top of `glare_catalog` that aims to provide
  Postgres compatability.
- `information_schema`: A set of views on top of `glare_catalog` for providing
  standard information schema compatability.

