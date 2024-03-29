---
layout: default
title: BigQuery
parent: Data Sources
---

<!-- markdownlint-disable MD022 -->

<!-- prettier-ignore-start -->
# BigQuery
{: .no_toc }
<!-- prettier-ignore-end -->

<!-- markdownlint-enable MD022 -->

BigQuery is able to be used as an external data source. Either an
entire database or a single table may be added as a data source.

<!-- prettier-ignore-start -->

- TOC
{:toc}
<!-- prettier-ignore-end -->

## Connect a BigQuery database

An entire BigQuery database can be added using the [CREATE EXTERNAL DATABASE]
command.

{: .important}

> `database-name` will be the name of the database inside GlareDB. This cannot be
> qualified, and must be unique across all other databases in the deployment.

```sql
CREATE EXTERNAL DATABASE <database-name>
 FROM bigquery
 OPTIONS (
  service_account_key = <gcp-service-account>,
  project_id = <gcp-project>,
 );
```

### Database options

| Field                 | Description                                               |
| --------------------- | --------------------------------------------------------- |
| `gcp-service-account` | The JSON encoded service account key.                     |
| `gcp-project`         | The GCP project containing the dataset/table of interest. |

## Connect a single table

Adding an external table can be done through the [CREATE EXTERNAL TABLE]
command.

```sql
CREATE EXTERNAL TABLE <table-name>
 FROM bigquery
 OPTIONS (
  service_account_key = <gcp-service-account>,
  project_id = <gcp-project>,
  dataset_id = <dataset-id>,
  table_id = <table-id>
 );
```

`table-name` will be the name of the table inside GlareDB. `table-name` may
optionally be qualified with a schema name.

### Table options

| Field                 | Description                                               |
| --------------------- | --------------------------------------------------------- |
| `gcp-service-account` | The JSON encoded service account key.                     |
| `gcp-project`         | The GCP project containing the dataset/table of interest. |
| `dataset-id`          | The ID of the dataset containing the table of interest.   |
| `table-id`            | The ID of the table to add to GlareDB.                    |

## Known issues

- Querying views defined in BigQuery is currently unsupported.

[CREATE EXTERNAL TABLE]: /reference/sql-commands/create-external-table
[CREATE EXTERNAL DATABASE]: /reference/sql-commands/create-external-database
