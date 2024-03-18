---
layout: default
title: CREATE EXTERNAL TABLE
parent: SQL commands
grand_parent: Reference
---

# CREATE EXTERNAL TABLE

Create an external table backed by a data source.

## Syntax

```sql
CREATE EXTERNAL TABLE [IF NOT EXISTS] <table-name>
    FROM <data-source-type>
    [TUNNEL <tunnel-name>]
    OPTIONS (<data-source-options>);
```

| Field                 | Description                                                                                                                                    |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| `table-name`          | Name of the database as it appears in GlareDB.                                                                                                 |
| `data-source-type`    | The type of data source: \[`bigquery`, `delta`, `gcs`, `iceberg`, `mongo`, `mysql`, `postgres`, `s3`, `snowflake`, `bson`, `lance`, `azure`\]. |
| `tunnel-name`         | [SSH tunnel] to connect with.                                                                                                                  |
| `data-source-options` | Options specific to this data source type.                                                                                                     |

`table-name` may optionally be qualified with a schema.

Specifying `IF NOT EXISTS` will suppress an error if `schema-name` already
exists.

## Examples

### Delta

In this example an external table named `my_delta_table` is created from a file
in GCS.

```sql
CREATE EXTERNAL TABLE my_delta_table
    FROM delta
    OPTIONS (
        location 'gs://<bucket_name>/<path_to_delta_table>',
        service_account_key '<gcp_service_account>'
    );
```

Alternatively, a [credentials object] can be created and used:

```sql
CREATE CREDENTIALS my_gcp_creds PROVIDER gcp
    ( service_account_key '<service_account_key>' );


CREATE EXTERNAL TABLE my_delta_table
    FROM delta
    CREDENTIALS my_gcp_creds
    OPTIONS (
        location 'gs://<bucket_name>/<path_to_delta_table>',
    );
```

### Postgres

In this example an external table named `external_table` is created using a
Postgres table `public.users` as a data source.

```sql
CREATE EXTERNAL TABLE external_table
    FROM postgres
    OPTIONS (
        host = 'my.postgres.host',
        port = '5432',
        user = 'glaredb',
        password = 'password',
        database = 'glaredb_test',
        schema = 'public',
        table = 'users'
    );
```

[SSH tunnel]: /docs/data-sources/securing-connections.html
[credentials object]: /glaredb/sql-commands/create-credentials/
