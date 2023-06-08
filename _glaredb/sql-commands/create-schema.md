---
layout: default
title: CREATE SCHEMA
parent: SQL commands
---

# CREATE SCHEMA

Create a schema in the `default` database.

## Syntax

```sql
CREATE SCHEMA [IF NOT EXISTS] <schema-name>;
```

| Field         | Description         |
| ------------- | ------------------- |
| `schema-name` | Name of the schema. |

Specifying `IF NOT EXISTS` will suppress an error if `schema-name` already
exists.

## Examples

Create a schema named `my_schema` if it doesn't already exist.

```sql
CREATE SCHEMA IF NOT EXISTS my_schema;
```
