---
layout: default
title: lance_scan
parent: SQL functions
grand_parent: Reference
---

# `lance_scan`

Read a lance table from the local filesystem or supported object store.

## Syntax

```sql
-- Single url or path.
lance_scan(<url>)
-- Using a cloud credentials object.
lance_scan(<url>, <credential_object>)
-- Required named argument for S3 buckets.
lance_scan(<url>, <credentials_object>, region => '<aws_region>')
-- Pass S3 credentials using named arguments.
lance_scan(<url>, access_key_id => '<aws_access_key_id>', secret_access_key => '<aws_secret_access_key>', region => '<aws_region>')
-- Pass GCS credentials using named arguments.
lance_scan(<url>, service_account_key => '<gcp_service_account_key>')
```

Parameter descriptions and which object store it's relevant to.

| Parameter                 | Object store | Description                                                                |
| ------------------------- | ------------ | -------------------------------------------------------------------------- |
| `url`                     | All          | The URL or path to a lance table to scan.                                  |
| `credential_object`       | S3 and GCS   | A database object storing credentials for accessing the object or objects. |
| `aws_region`              | S3           | If scanning an object in S3, the region of the bucket.                     |
| `aws_access_key_id`       | S3           | ID of AWS access key with permissions to read from the bucket.             |
| `aws_secret_access_key`   | S3           | Secret associated with the AWS access key.                                 |
| `gcp_service_account_key` | GCS          | A JSON-encoded GCP service account key with access to the bucket.          |

The path or URL provided to `lance_scan`
should be to a directory containing a [lance dataset]

## Usage

### Local files

Local lance table can be read with `lance_scan` by passing in a path to the
table. Paths may be absolute or relative.

```sql
-- Read a relative path.
SELECT * FROM lance_scan('./directory/my_lance_table/');
```

### Objects in GCS

Objects in GCS can be read by providing the path to the object and credentials
for the object to `lance_scan`. The service account key provided should be
JSON encoded.

```sql
-- Single object.
SELECT * FROM lance_scan('gs://my-bucket/path/lance_table',
                           service_account_key => '<service_account_key>');
```

Optionally, a credentials object can be created and used in place of providing
the service account key directly.

```sql
-- Create the credentials.
CREATE CREDENTIALS my_gcp_creds PROVIDER gcp
    ( service_account_key '<service_account_key>' );
-- And use them in the scan.
SELECT * FROM lance_scan('gs://my-bucket/path/lance_table', my_gcp_creds);
```

### Objects in S3

Objects in GCS can be read by providing the path to the object and credentials
for the object, and the bucket region to `lance_scan`.

```sql
SELECT * FROM lance_scan('gs://my-bucket/path/lance_table',
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
SELECT * FROM lance_scan('gs://my-bucket/path/lance_table', my_aws_creds, region => 'us-east-1');
```

[lance dataset]: https://lancedb.github.io/lance/format.html#dataset-directory
