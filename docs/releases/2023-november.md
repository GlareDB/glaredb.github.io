---
layout: default
title: November 2023
parent: "Release notes"
nav_order: 4
---

# November 2023

{:.important}

> To use Hybrid Execution, all clients (Python, GlareDB CLI) must update to
> 0.7.0+. TLS was enabled and made _required_ for Hybrid Execution.

## Microsoft SQL Server

**Available in**: [GlareDB@v0.7.0], [GlareDB Cloud]

GlareDB now supports SQL Server as an external data source. You can configure
[EXTERNAL TABLE](/docs/data-sources/supported/sql-server.html#add-a-single-table)s
and [EXTERNAL DATABASE](/docs/data-sources/supported/sql-server.html#add-a-sql-server-database)s
from SQL Server.

## Azure Blob Storage

**Available in**: [GlareDB@v0.7.0], [GlareDB Cloud]

GlareDB can now use CSV, ndjson, or Parquet files in Azure Blob Storage as
external tables:

```sql
CREATE EXTERNAL TABLE my_azure_source
 FROM azure
 OPTIONS (
  account_name = '<azure-account>',
  access_key = '<access-key>'
  location = 'azure://<storage-container>/<object-path>'
);
```

## Node bindings

**Available in**: [GlareDB@v0.7.0]

GlareDB is now available in Node.js and distributed via [npm]:

```shell
npm i @glaredb/glaredb
```

```js
// CommonJS
const glaredb = require("@glaredb/glaredb");

let con = await glaredb.connect();
let res = await con.sql("SELECT 'hello JS'");
await res.show();

// ESM
import glaredb from "@glaredb/glaredb";

let con = await glaredb.connect();
let res = await con.sql("SELECT 'hello JS'");
await res.show();
```

## Table functions

**Available in**: [GlareDB@v0.7.0], [GlareDB Cloud]

- Tildes (`~`) in paths are now properly expanded

**Available in**: [GlareDB@v0.6.1], [GlareDB Cloud]

- `read_excel` to read `.xlsx` files:

  ```sql
  select * from read_excel('file://data.xlsx')
  ```

## SQL improvements

**Available in**: [GlareDB@v0.7.0], [GlareDB Cloud]

- Set `READ_WRITE` and `READ_ONLY` modes for external databases and tables. By
  setting a database or table to `READ_ONLY`, inserts are not permitted.

  ```sql
  ALTER DATABASE <database> SET ACCESS_MODE TO READ_WRITE;
  ALTER TABLE <table> SET ACCESS_MODE TO READ_ONLY;
  ```

**Available in**: [GlareDB@v0.6.1], [GlareDB Cloud]

- `DESCRIBE` supports describing tables

  ```sql
  DESCRIBE my_table
  ```

## Python improvements

**Available in**: [GlareDB@v0.7.0]

- A convenient `prql` method was added that can be called without setting the
  current dialect

  ```py
  import glaredb
  con = glaredb.connect()
  con.prql('<my prql query>').show()
  ```

[GlareDB@v0.6.1]: https://github.com/GlareDB/glaredb/releases/tag/v0.6.1
[GlareDB@v0.7.0]: https://github.com/GlareDB/glaredb/releases/tag/v0.7.0
[GlareDB Cloud]: https://console.glaredb.com
[npm]: https://www.npmjs.com/package/@glaredb/glaredb
