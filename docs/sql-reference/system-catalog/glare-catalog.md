---
layout: default
title: glare_catalog
parent: System catalog
grand_parent: SQL reference
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

[CREATE EXTERNAL TABLE]: {{site.baseurl}}/docs/sql-commands/create-external-table
[CREATE EXTERNAL DATABASE]: {{site.baseurl}}/docs/sql-commands/create-external-database
