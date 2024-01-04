---
layout: default
title: January 2024
parent: "Release notes"
nav_order: 6
---

# January 2024

## ClickHouse

**Available in**: [GlareDB@v0.8.0], [GlareDB Cloud]

GlareDB now supports ClickHouse as an external data source. Learn more in our
[ClickHouse docs](/docs/data-sources/supported/clickhouse).

## Table functions

**Available in**: [GlareDB@v0.8.0], [GlareDB Cloud]

- `read_sqlserver` to read tables from SQL Server:

  ```sql
  select * from read_sqlserver(
    'server=tcp:my.sqlserver.host,1433;user=SA;password=Password123;TrustServerCertificate=true',
    'dbo',
    'users'
  );
  ```

[GlareDB Cloud]: https://console.glaredb.com
[GlareDB@v0.8.0]: https://github.com/GlareDB/glaredb/releases/tag/v0.8.0
