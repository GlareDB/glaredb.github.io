---
layout: default
title: GCS
parent: Data Sources
---

<!-- markdownlint-disable MD022 -->

<!-- prettier-ignore-start -->
# GCS
{: .no_toc }
<!-- prettier-ignore-end -->

<!-- markdownlint-enable MD022 -->

CSV and Parquet files in GCS storage are able to be used as an external data
source.

<!-- prettier-ignore-start -->

- TOC
{:toc}
<!-- prettier-ignore-end -->

## GCS file as an external table

CSV and Parquet files can be added as an external table through the
[CREATE EXTERNAL TABLE] command.

{: .important}

> `table-name` will be the name of the database inside GlareDB. `table-name` may
> optionally be qualified with a schema name.

```sql
CREATE EXTERNAL TABLE <table-name>
 FROM gcs
 OPTIONS (
  service_account_key = '<service-account-key>',
  bucket = '<bucket>',
  location = '<location>'
);
```

### Table options

| Field                 | Description                                       |
| --------------------- | ------------------------------------------------- |
| `service_account_key` | A [Service Account] with access to the bucket     |
| `bucket`              | The name of the bucket                            |
| `location`            | The path to the file, relative to the bucket root |

<!-- markdownlint-disable line-length -->

[CREATE EXTERNAL TABLE]: /glaredb/sql-commands/create-external-table
[Service Account]: https://cloud.google.com/iam/docs/service-account-overview

<!-- markdownlint-enable line-length -->
