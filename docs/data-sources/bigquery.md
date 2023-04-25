---
layout: default
title: BigQuery
parent: Data sources
---

# BigQuery

BigQuery is able to be used as an external data source. Either a table or an
entire database may be added as a data source.

## External table

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

### Options

| Field                 | Description                                               |
| --------------------- | --------------------------------------------------------- |
| `gcp-service-account` | The JSON encoded service account key.                     |
| `gcp-project`         | The GCP project containing the dataset/table of interest. |
| `dataset-id`          | The ID of the dataset containing the table of interes.    |
| `table-id`            | The ID of the table to add to GlareDB.                    |

## External database

An entire BigQuery database can be added using the [CREATE EXTERNAL DATABASE]
command.

```sql
CREATE EXTERNAL DATABASE <database-name>
	FROM bigquery
	OPTIONS (
		service_account_key = <gcp-service-account>,
		project_id = <gcp-project>,
	);
```

`database-name` will be the name of the database inside GlareDB. This cannot be
qualified, and must be unique across all other databases in the deployment.

### Options

| Field                 | Description                                               |
| --------------------- | --------------------------------------------------------- |
| `gcp-service-account` | The JSON encoded service account key.                     |
| `gcp-project`         | The GCP project containing the dataset/table of interest. |

## Known issues

- Querying views defined in BigQuery is currently unsupported.

[CREATE EXTERNAL TABLE]:
  {{site.baseurl}}/docs/sql-commands/create-external-table
[CREATE EXTERNAL DATABASE]:
  {{site.baseurl}}/docs/sql-commands/create-external-database
