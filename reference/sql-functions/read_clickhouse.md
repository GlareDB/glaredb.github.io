---
layout: default
title: read_clickhouse
parent: SQL functions
grand_parent: Reference
---

# `read_clickhouse`

Read a ClickHouse table. The table does not have to be a known data source to
GlareDB.

## Syntax

```sql
read_clickhouse(<connection_string>, <table>)
```

| Field               | Description                     |
| ------------------- | ------------------------------- |
| `connection_string` | A ClickHouse connection string. |
| `table`             | The name of the table to query. |

## Examples

In the following example, a 'users' table located in a ClickHouse database is
queryed.

```sql
select * from read_clickhouse(
  'clickhouse://my_user:my_password@my.clickhouse.host:9000/default',
  'users'
);
```

Refer to the [documentation on ClickHouse data sources] for more information.

[documentation on ClickHouse data sources]: /data-sources/clickhouse
