---
layout: default
title: Azure Blob Storage
parent: Data Sources
---
# Azure Blob Storage

GlareDB can use CSV, ndjson, or Parquet files in Azure Blob Storage as external
data sources.

## Azure File as an External Table

Add CSV, ndjson, or Parquet files as an external table with the
[CREATE EXTERNAL TABLE] command.

{: .important}

> `table-name` becomes the name of the database inside GlareDB. `table-name` can
> be qualified with a schema name.

```sql
CREATE EXTERNAL TABLE <table-name>
 FROM azure
 OPTIONS (
  account_name = '<azure-account>',
  access_key = '<access-key>'
  location = 'azure://<storage-container>/<object-path>'
);
```

### Table options

| Field               | Description                                                |
| ------------------- | ---------------------------------------------------------- |
| `account_name`      | Name of the Azure account containing the storage container |
| `access_key`        | Access key for the storage container                       |
| `storage-container` | Storage container containing the object                    |
| `object-path`       | Path to the object inside the storage container            |

<!-- markdownlint-disable line-length -->

[CREATE EXTERNAL TABLE]: /glaredb/sql-commands/create-external-table

<!-- markdownlint-enable line-length -->
