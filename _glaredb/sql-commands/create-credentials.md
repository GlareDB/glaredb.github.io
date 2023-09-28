---
layout: default
title: CREATE CREDENTIALS
parent: SQL commands
---

# CREATE CREDENTIALS

Create credentials for accessing AWS and Google Cloud resources.

## Syntax

```sql
CREATE CREDENTIALS <credential-name>
    PROVIDER <provider>
    OPTIONS (<provider-options>);
```

| Field              | Description                                                        |
| ------------------ | ------------------------------------------------------------------ |
| `credential-name`  | Name for the credentials.                                          |
| `provider`         | Cloud provider these credentials are for. Values: \[`aws`, `gcp`\] |
| `provider-options` | Provider specific options. See below.                              |

## AWS credentials

AWS credentials allow GlareDB to read and write objects in S3.

Creating AWS credentials requires `access_key_id` and `secret_access_key`. These
correspond to an IAM user with permissions for accessing objects in S3.

```sql
CREATE CREDENTIALS my_aws_creds
PROVIDER aws
OPTIONS (
    access_key_id = 'my_access_key_id',
    secret_access_key = 'my_secret_access_key',
);
```

After creating the credentials, they can be used to access objects in S3:

```sql
SELECT * FROM parquet_scan(
    's3://my_bucket/data/*.parquet',
    my_aws_creds,
    region => 'us-east-1'
);
```

As another example, the credentials can be used to write output of a query to
S3:

```sql
COPY ( SELECT 5 AS a, 6 AS b )
TO 's3://my_bucket/data/output.parquet'
CREDENTIALS my_aws_creds ( region 'us-east-1' );
```

These examples require specifying `region`. GlareDB requires a `region` when
connecting to an S3 resource. Use the AWS region of the bucket.

## GCP credentials

GCP credentials allow GlareDB to read and write objects in GCS.

The **service_account_key** option is required when creating GCP credentials.
service_account_key is a JSON-encoded key for a service account. Only buckets
that this service account has read permissions for can be queryed.

```sql
CREATE CREDENTIALS my_gcp_creds
PROVIDER gcp
OPTIONS (
    service_account_key = 'my_gcp_service_account_key',
);
```

After creating the credentials, they can be used to access objects in GCS:

```sql
SELECT * FROM parquet_scan(
    'gs://my_bucket/data/*.parquet',
    my_gcp_creds
);
```

As another example, the credentials can be used to write output of a query to
GCS:

```sql
COPY ( SELECT 5 AS a, 6 AS b )
TO 'gs://my_bucket/data/output.parquet'
CREDENTIALS my_gcp_creds;
```
