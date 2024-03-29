---
layout: default
title: ALTER TABLE
parent: SQL commands
grand_parent: Reference
---

# ALTER TABLE

Alter a table. Builtin system tables cannot be altered. See [system
catalog] for an overview of builtin tables and views.

With this command, GlareDB supports:

- renaming a table
- setting the access mode of an external table

## Syntax

```sql
ALTER TABLE <table-name>
  [RENAME TO <new-name>]
  [SET ACCESS_MODE TO <access-mode>];
```

| Field         | Description                           |
| ------------- | ------------------------------------- |
| `table-name`  | Name of the table to rename.          |
| `new-name`    | New name for the table.               |
| `access-mode` | One of: \[`READ_WRITE`, `READ_ONLY`\] |

`table-name` may optionally be qualified with a schema.

## Examples

Rename table `t1` to `t2`. See [CREATE EXTERNAL TABLE] for adding a table.

```sql
ALTER TABLE t1 RENAME TO t2;
```

Add an Azure external table and set it to `READ_ONLY`. See [Azure Blob Storage]
and [CREATE EXTERNAL TABLE] for more details.

```sql
CREATE EXTERNAL TABLE my_azure_table
 FROM azure
 OPTIONS (
  account_name = '<azure-account>',
  access_key = '<access-key>'
  location = 'azure://<storage-container>/<object-path>'
);

ALTER TABLE my_azure_table SET ACCESS_MODE TO READ_ONLY;
```

[CREATE EXTERNAL TABLE]: /reference/sql-commands/create-external-table/
[system catalog]: /glaredb/system-catalog/index/
[Azure Blob Storage]: /data-sources/azure
