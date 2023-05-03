---
layout: default
title: information_schema
parent: System catalog
grand_parent: SQL reference
---

# `information_schema`

Traditionally, an `information_schema` contains views of the metadata on
internal objects, such as internal columns and tables.

## View internal columns

Presently only `glare_catalog` columns are selected.

```sql
select table_schema, table_name, column_name
from information_schema.columns;
```

```text
 table_schema  |      table_name       |    column_name
---------------+-----------------------+--------------------
 glare_catalog | databases             | oid
 glare_catalog | databases             | database_name
 glare_catalog | databases             | builtin
 glare_catalog | databases             | external
 glare_catalog | databases             | datasource
 glare_catalog | schemas               | oid
 glare_catalog | schemas               | database_oid
 glare_catalog | schemas               | database_name
 glare_catalog | schemas               | schema_name
 glare_catalog | schemas               | builtin
 glare_catalog | session_query_metrics | query_text
 glare_catalog | session_query_metrics | result_type
 glare_catalog | session_query_metrics | execution_status
 glare_catalog | session_query_metrics | error_message
 glare_catalog | session_query_metrics | elapsed_compute_ns
 glare_catalog | session_query_metrics | output_rows
 glare_catalog | columns               | schema_oid
 glare_catalog | columns               | table_oid
 glare_catalog | columns               | table_name
 glare_catalog | columns               | column_name
 glare_catalog | columns               | column_ordinal
 glare_catalog | columns               | data_type
 glare_catalog | columns               | is_nullable
 glare_catalog | tables                | oid
 glare_catalog | tables                | database_oid
 glare_catalog | tables                | schema_oid
 glare_catalog | tables                | schema_name
 glare_catalog | tables                | table_name
 glare_catalog | tables                | builtin
 glare_catalog | tables                | external
 glare_catalog | tables                | datasource
 glare_catalog | views                 | oid
 glare_catalog | views                 | database_oid
 glare_catalog | views                 | schema_oid
 glare_catalog | views                 | schema_name
 glare_catalog | views                 | view_name
 glare_catalog | views                 | builtin
 glare_catalog | views                 | sql
(38 rows)
```

## View internal tables

```sql
select table_schema, table_name
from information_schema.tabes;
```

```text
    table_schema    |      table_name
--------------------+-----------------------
 pg_catalog         | pg_attribute
 pg_catalog         | pg_description
 information_schema | columns
 glare_catalog      | external_datasources
 pg_catalog         | pg_namespace
 information_schema | tables
 pg_catalog         | pg_table
 pg_catalog         | pg_am
 pg_catalog         | pg_views
 pg_catalog         | pg_class
 pg_catalog         | pg_database
 information_schema | schemata
 glare_catalog      | databases
 glare_catalog      | schemas
 glare_catalog      | session_query_metrics
 glare_catalog      | columns
 glare_catalog      | tables
 glare_catalog      | views
(18 rows)
```
