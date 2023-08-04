---
layout: default
title: iceberg_scan
parent: SQL functions
---

# `iceberg_scan`

Read an Iceberg table from the local filesystem or support object store.

Iceberg support is early. Additional Iceberg related features are being tracked
in [Issue #1448].

## Syntax

```sql
-- Single url or path.
iceberg_scan(<url>)
-- Using a cloud credentials object.
iceberg_scan(<url>, <credential_object>)
-- Required named argument for S3 buckets.
iceberg_scan(<url>, <credentials_object>, region => '<aws_region>')
-- Pass S3 credentials using named arguments.
iceberg_scan(<url>, access_key_id => '<aws_access_key_id>', secret_access_key => '<aws_secret_access_key>', region => '<aws_region>')
-- Pass GCS credentials using named arguments.
iceberg_scan(<url>, service_account_key => '<gcp_service_account_key>')
```

Parameter descriptions and which object store it's relevant to.

| Parameter                 | Object store | Description                                                                |
| ------------------------- | ------------ | -------------------------------------------------------------------------- |
| `url`                     | All          | The URL or path to a iceberg table to scan.                                |
| `credential_object`       | S3 and GCS   | A database object storing credentials for accessing the object or objects. |
| `aws_region`              | S3           | If scanning an object in S3, the region of the bucket.                     |
| `aws_access_key_id`       | S3           | ID of AWS access key with permissions to read from the bucket.             |
| `aws_secret_access_key`   | S3           | Secret associated with the AWS access key.                                 |
| `gcp_service_account_key` | GCS          | A JSON-encoded GCP service account key with access to the bucket.          |

The path or URL provided to `iceberg_scan` should be to a directory containing
the `metadata/` and `data/` directories for the table.

## Usage

### Local files

Local Iceberg table can be read with `iceberg_scan` by passing in a path to the
table. Paths may be absolute or relative.

```sql
-- Read a relative path.
SELECT * FROM iceberg_scan('./directory/my_iceberg_table/');
```

### Objects in GCS

Objects in GCS can be read by providing the path to the object and credentials
for the object to `iceberg_scan`. The service account key provided should be
JSON encoded.

```sql
-- Single object.
SELECT * FROM iceberg_scan('gs://my-bucket/path/iceberg_table',
                           service_account_key => '<service_account_key>');
```

Optionally, a credentials object can be created and used in place of providing
the service account key directly.

```sql
-- Create the credentials.
CREATE CREDENTIALS my_gcp_creds PROVIDER gcp
    ( service_account_key '<service_account_key>' );
-- And use them in the scan.
SELECT * FROM iceberg_scan('gs://my-bucket/path/iceberg_table', my_gcp_creds);
```

### Objects in S3

Objects in GCS can be read by providing the path to the object and credentials
for the object, and the bucket region to `iceberg_scan`.

```sql
SELECT * FROM iceberg_scan('gs://my-bucket/path/iceberg_table',
                           access_key_id = '<access_key_id>',
                           secret_access_key = '<secret_access_key>',
                           region = 'us-east-1');
```

Optionally, a credentials object can be created and used in place of providing
the service account key directly.

```sql
-- Create the credentials.
CREATE CREDENTIALS my_aws_creds PROVIDER aws
    OPTIONS (
        access_key_id = '<access_key_id>',
        secret_access_key = '<secret_access_key>',
    );
-- And use them in the scan. Note that a region still needs to be provided.
SELECT * FROM iceberg_scan('gs://my-bucket/path/iceberg_table', my_aws_creds, region => 'us-east-1');
```

[Issue #1448]: https://github.com/GlareDB/glaredb/issues/1448
