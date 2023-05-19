---
layout: default
title: pg_catalog
parent: System catalog
grand_parent: SQL reference
---

# `pg_catalog`

In order to be Postgres-compatible, GlareDB implements a large portion of the
[Postgres catalog]. While we are not yet fully-compatible, (see: [Technical Preview]),
GlareDB operates with `psql` and popular BI Tools.

## Viewing `pg_catalog` tables

```sql
select table_name
from information_schema.tables
where table_schema = 'pg_catalog';
```

```text
   table_name
----------------
 pg_attribute
 pg_description
 pg_namespace
 pg_table
 pg_am
 pg_views
 pg_class
 pg_database
(8 rows)
```

[Postgres catalog]: https://www.postgresql.org/docs/current/catalogs.html
[Technical Preview]: /docs/about/technical-preview.html
