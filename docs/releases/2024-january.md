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

## Dashboard updates

**Available in**: [GlareDB Cloud]

- The SQL Workspace explorer now has search and shows richer table and column
  information

  ![SQL Workspace]

- GlareDB Cloud now supports signing in with GitHub

  ![Signin]

- The Connection Dialog got reworked and now contains Node.js and other examples

  ![Connect Dialog]

## Misc updates and fixes

**Available in**: [GlareDB@v0.8.0], [GlareDB Cloud]

- Fix reading Iceberg tables with a large version number
  ([#2281](https://github.com/GlareDB/glaredb/pull/2281))

[GlareDB Cloud]: https://console.glaredb.com
[GlareDB@v0.8.0]: https://github.com/GlareDB/glaredb/releases/tag/v0.8.0
[SQL Workspace]: /assets/images/release-notes/2024-january/sql_workspace.png
[Signin]: /assets/images/release-notes/2024-january/signin.png
[Connect Dialog]: /assets/images/release-notes/2024-january/connect_dialog.png
