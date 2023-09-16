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

| Field              | Description                                                       |
| ------------------ | ----------------------------------------------------------------- |
| `credential-name`  | Name for the credentials.                                         |
| `provider`         | The cloud provider for these credentials are for. `aws` or `gcp`. |
| `provider-options` | Provider specific options. See below sections.                    |

## AWS credentials

AWS credentials allows GlareDB to read and write objects in S3.

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

We can use the above credentials to access objects in S3:

```sql
SELECT * FROM parquet_scan('s3://my_bucket/data/*.parquet', my_aws_creds, region => 'us-east-1');
```

We can also use credentials to copy output of a query to S3:

```sql
COPY ( SELECT 5 AS a, 6 AS b )
    TO 's3://my_bucket/data/output.parquet'
    CREDENTIALS my_aws_creds
    ( region 'us-east-1' );
```

Note that both of these example require specifying `region`. This is required
when interacting with S3, and should be the AWS region where the bucket is
located.

## GCP credentials

GCP credentials allows GlareDB to readn and write objects in GCS.

Creating GCP credentials requires `service_account_key` to be provided as an
option. This should be a JSON encoded key for a service account with access to
the GCS buckets you'll want to query.

```sql
CREATE CREDENTIALS my_gcp_creds
    PROVIDER gcp
    OPTIONS (
        service_account_key = 'my_gcp_service_account_key',
    );
```

We can use the above credentials to access objects in GCS:

```sql
SELECT * FROM parquet_scan('gs://my_bucket/data/*.parquet', my_gcp_creds);
```

We can also use credentials to copy output of a query to GCS:

```sql
COPY ( SELECT 5 AS a, 6 AS b )
    TO 'gs://my_bucket/data/output.parquet'
    CREDENTIALS my_gcp_creds;
```
