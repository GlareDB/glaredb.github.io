---
layout: default
title: glare_catalog
parent: System catalog
---

<!-- markdownlint-disable MD022 -->

<!-- prettier-ignore-start -->
# `glare_catalog`
{: .no_toc }
<!-- prettier-ignore-end -->

<!-- markdownlint-enable MD022 -->

The `glare_catalog` schema provides a variety of tables and views for allowing
introspection into the system.

{: .warning}

> `glare_catalog` does not currently have any stability guarantees.

<!-- prettier-ignore -->
- TOC
{:toc}

## `databases`

Stores information about databases.

| Field           | Description                                                             |
| --------------- | ----------------------------------------------------------------------- |
| `oid`           | Internal identifier for this object.                                    |
| `database_name` | Name of the database inside GlareDB.                                    |
| `builtin`       | If this database is builtin.                                            |
| `external`      | If this database is external (created with [CREATE EXTERNAL DATABASE]). |
| `datasource`    | The data source type for this database (e.g. "postgres").               |

## `schemas`

Stores information about schemas.

| Field           | Description                                         |
| --------------- | --------------------------------------------------- |
| `oid`           | Internal identifier for this object.                |
| `database_oid`  | Identifier for the database containing this schema. |
| `database_name` | Name of the owning database.                        |
| `schema_name`   | Name of the schema.                                 |
| `builtin`       | If this schema is builtin.                          |

## `tables`

Stores information about tables.

| Field          | Description                                                          |
| -------------- | -------------------------------------------------------------------- |
| `oid`          | Internal identifier for this object.                                 |
| `database_oid` | Identifier for the database containing this table.                   |
| `schema_oid`   | Identifier for the schema containing this table.                     |
| `schema_name`  | Name of the schema containing this table.                            |
| `table_name`   | Name of the table.                                                   |
| `builtin`      | If this table is builtin.                                            |
| `external`     | If this database is external (created with [CREATE EXTERNAL TABLE]). |
| `datasource`   | The data source type for this table (e.g. "postgres").               |

## `views`

Stores information about views.

| Field          | Description                                       |
| -------------- | ------------------------------------------------- |
| `oid`          | Internal identifier for this object.              |
| `database_oid` | Identifier for the database containing this view. |
| `schema_oid`   | Identifier for the schema containing this view.   |
| `schema_name`  | Name of the schema containing this view.          |
| `view_name`    | Name of the view.                                 |
| `builtin`      | If this view is builtin.                          |
| `sql`          | The SQL statement for this view.                  |

## `columns`

Stores information about columns.

| Field            | Description                                               |
| ---------------- | --------------------------------------------------------- |
| `schema_oid`     | Identifier for the schema containing this column's table. |
| `table_oid`      | Identifier for the table containing this column.          |
| `table_name`     | Name of the table containing this column.                 |
| `column_name`    | Name of the column.                                       |
| `column_ordinal` | Position of this column.                                  |
| `data_type`      | Data type of this column.                                 |
| `is_nullable`    | If this column is nullable.                               |

## `tunnels`

Stores information about [SSH tunnels].

| Field         | Description                          |
| ------------- | ------------------------------------ |
| `oid`         | Internal identifier for this object. |
| `tunnel_name` | Name of the tunnel.                  |
| `builtin`     | If this tunnel is builtin.           |
| `tunnel_type` | Type of the tunnel (ex: `ssh`)       |

## `ssh_keys`

Stores information about public keys associated to `tunnels`.

| Field             | Description                     |
| ----------------- | ------------------------------- |
| `ssh_tunnel_oid`  | `oid` of the `tunnel`           |
| `ssh_tunnel_name` | `tunnel_name` of the `tunnel`   |
| `public_key`      | Public SSH key for the `tunnel` |

## `functions`

Stores information about built-in glaredb functions that are useful for working
with and generating data. Each of these functions can be used in queries.

For more information on a specific function, refer to its reference:

- [`csv_scan`]
- [`delta_scan`]
- [`lance_scan`]
- [`generate_series`]
- [`list_schemas`]
- [`list_tables`]
- [`ndjson_scan`]
- [`parquet_scan`]
- [`read_bigquery`]
- [`read_mongodb`]
- [`read_mysql`]
- [`read_postgres`]
- [`read_snowflake`]

| Field             | Descriptions                                              |
| ----------------- | --------------------------------------------------------- |
| `oid`             | Internal identifier for this object.                      |
| `schema_oid`      | Identifier for the schema containing this column's table. |
| `function_name`   | The name (keyword) of the function                        |
| `function_type`   | Currently all functions are of type `table`.              |
| `parameters`      | Currently not implemented.                                |
| `parameter_types` | Currently not implemented.                                |
| `builtin`         | Indicates if this function is built into GlareDB          |

[CREATE EXTERNAL TABLE]: /glaredb/sql-commands/create-external-table.html
[CREATE EXTERNAL DATABASE]: /glaredb/sql-commands/create-external-database.html
[SSH tunnels]: /docs/data-sources/overview.html#securing-connections-with-ssh-tunnels
[`csv_scan`]: /glaredb/sql-commands/csv_scan
[`delta_scan`]: /glaredb/sql-commands/delta_scan
[`lance_scan`]: /glaredb/sql-commands/lance_scan
[`generate_series`]: /glaredb/sql-commands/generate_series
[`list_schemas`]: /glaredb/sql-commands/list_schemas
[`list_tables`]: /glaredb/sql-commands/list_tables
[`ndjson_scan`]: /glaredb/sql-commands/ndjson_scan
[`parquet_scan`]: /glaredb/sql-commands/parquet_scan
[`read_bigquery`]: /glaredb/sql-commands/read_bigquery
[`read_mongodb`]: /glaredb/sql-commands/read_mongodb
[`read_mysql`]: /glaredb/sql-commands/read_mysql
[`read_postgres`]: /glaredb/sql-commands/read_postgres
[`read_snowflake`]: /glaredb/sql-commands/read_snowflake
