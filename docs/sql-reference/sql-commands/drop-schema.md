---
layout: default
title: DROP SCHEMA
parent: SQL commands
grand_parent: SQL reference
---

<!-- markdownlint-disable title-case-style -->

# DROP SCHEMA

<!-- markdownlint-enable title-case-style -->

Drop a schema. Note that builtin schemas cannot be dropped. See [system catalog]
for an overview of builtin schemas.

## Syntax

```sql
DROP SCHEMA [IF EXISTS] <schema-name> [CASCADE];
```

| Field        | Description        |
| ------------ | ------------------ |
| `table-name` | The table to drop. |

`schema-name` may optionally be qualified with a schema name.

If `CASCADE` is specified, all child tables and views will also be dropped. If
`CASCADE` is omitted, the command will error if any tables or views exist in the
schema.

## Examples

Drop a schema named `my_schema`, also dropping all tables and views within that
schema. See [CREATE SCHEMA] for how to create a schema.

```sql
DROP SCHEMA my_schema CASCADE;
```

[CREATE SCHEMA]: {{site.baseurl}}/docs/sql-commands/create-schema
[system catalog]: {{site.baseurl}}/docs/system-catalog
