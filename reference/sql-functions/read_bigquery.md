---
layout: default
title: read_bigquery
parent: SQL functions
grand_parent: Reference
---

# `read_bigquery`

Read a BigQuery table. The table does not have to be a known data source to
GlareDB. As long as you can access the table with a service account, it can be
queried.

## Syntax

```sql
read_bigquery(<gcp_service_account_key>, <project_id>, <dataset_id>, <table_id>)
```

| Field                     | Description                                       |
| ------------------------- | ------------------------------------------------- |
| `gcp_service_account_key` | The JSON encoded service account key.             |
| `project_id`              | The GCP project containing the table of interest. |
| `dataset_id`              | The dataset ID where the table resides            |
| `table_id`                | The table ID                                      |

## Examples

In the following example, a 'users' table located in a BigQuery project is
queryed.

```sql
select * from read_bigquery(
  '{<your_service_account_key>}',
  'example-bigquery-project',
  'example-dataset',
  'users'
);
```
