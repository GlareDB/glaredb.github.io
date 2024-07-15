---
layout: default
title: COPY TO
parent: SQL commands
grand_parent: Reference
---

# COPY TO

Copy rows from a table or query to local files or supported object stores.

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Syntax

```sql
-- Copy the output of a query, or table, to a local path
COPY [(<query>) | <table>] TO '<location>' [FORMAT format];
-- Alternative syntax for local copying
COPY [(<query>) | <table>] TO LOCAL [FORMAT format] OPTIONS (
  location = '<location>'
);

-- Copy the output of a query or table to GCS
COPY [(<query>) | <table>] TO gcs [FORMAT format] OPTIONS (
  bucket = '<bucket>',
  location = '<location>',
  service_account_key = '<gcp_service_account_key>'
)
-- Alternative syntax for copying to GCS with OPTIONS
COPY [(<query>) | <table>] TO '<gcs_url>' [FORMAT format] OPTIONS (
  service_account_key = '<gcp_service_account_key>'
);
-- Alternative syntax for copying to GCS with a CREDENTIALS database object
COPY [(<query>) | <table>] TO '<gcs_url>' [FORMAT format]
CREDENTIALS gcp_credentials;

-- Copy the output of a query or table to S3 with OPTIONS
COPY [(<query>) | <table>] TO s3 [FORMAT format] OPTIONS (
  access_key_id = '<aws_access_key_id>',
  bucket = '<bucket>',
  location = '<location>',
  region = '<aws_region>',
  secret_access_key = '<aws_secret_access_key>'
);
-- Alternative syntax for copying S3 with OPTIONS
COPY [(<query>) | <table>] TO '<s3_url>' [FORMAT format] OPTIONS (
        access_key_id = '<aws_access_key_id>',
        region = '<aws_region>',
        secret_access_key = '<aws_secret_access_key>'
);
-- Alternative syntax for copying to S3 with a CREDENTIALS database object
COPY [(<query>) | <table>] TO '<s3_url>' [FORMAT format]
CREDENTIALS s3_credentials ( region '<aws_region>' );
```

| Field                     | Destination | Description                                                                  |
| ------------------------- | ----------- | ---------------------------------------------------------------------------- |
| `aws_region`              | S3          | The region of the bucket.                                                    |
| `aws_access_key_id`       | S3          | ID of AWS access key with permissions to write the bucket.                   |
| `aws_secret_access_key`   | S3          | Secret associated with the AWS access key.                                   |
| `bucket`                  | GCS or S3   | Name of the bucket.                                                          |
| `format`                  | All         | Output format. One of **csv** (default), **json**, **bson**, or **parquet**. |
| `gcp_credentials`         | GCS         | A database object containing GCP credentials.                                |
| `gcp_service_account_key` | GCS         | A JSON-encoded GCP service account key with access to the bucket.            |
| `gcs_url`                 | GCS         | A url in the format gs://bucket/location                                     |
| `location`                | All         | A path to copy to.                                                           |
| `query`                   | All         | The query to execute, of which the results will be copied.                   |
| `s3_credentials`          | S3          | A database object containing S3 credentials.                                 |
| `s3_url`                  | S3          | A url in the format s3://bucket/location                                     |
| `table`                   | All         | A fully-qualified table name.                                                |

## Usage

### Local files

A query or table may be copied to a local file.

```sql
-- copy the result of 'select 1' to result.parquet in the current directory
COPY (select 1) TO 'result.parquet' FORMAT parquet;
-- Same as above with OPTIONS syntax
COPY (select 1) TO LOCAL FORMAT parquet OPTIONS (location = 'result.parquet');
-- copy all rows of the users table to /tmp/users.json
COPY public.users TO '/tmp/users.json' FORMAT json;
-- Same as above with OPTIONS syntax
COPY public.users TO LOCAL FORMAT json OPTIONS (location = '/tmp/users.json');
```

### Copying files to GCS

Files in GCS can be copied to by providing the path to the file and credentials.
The service account key provided should be JSON encoded.

```sql
-- copy the result of 'select 1' to results.csv in a bucket
COPY ( SELECT 1 ) TO gcs OPTIONS (
  bucket = 'bucket',
  location = 'results.csv'
  service_account_key = 'gcp_service_account_key',
);
-- same as above, but using a URL and OPTIONS
COPY ( SELECT 1 ) TO 'gs://bucket/results.csv' OPTIONS (
  service_account_key = 'gcp_service_account_key'
);
```

Optionally, a credentials object can be created and used in place of providing
the service account key directly.

```sql
-- Create the credentials.
CREATE CREDENTIALS my_gcp_creds PROVIDER gcp (
  service_account_key '<service_account_key>'
);
-- And use them in copy public.users.
COPY public.users TO 'gs://bucket/users.json' FORMAT json
CREDENTIALS my_gcp_creds;
```

### Copying files to S3

Files in S3 can be copied to by providing the path to the file and credentials.

```sql
-- copy the result of 'select 1' to results.csv in a bucket
COPY ( SELECT 1 ) TO s3 OPTIONS (
  access_key_id = '<aws_access_key_id>',
  bucket = '<bucket>',
  location = 'results.csv',
  region = '<aws_region>',
  secret_access_key = '<aws_secret_access_key>'
);
-- same as above, but using a URL and OPTIONS
COPY ( SELECT 1 ) TO 's3://bucket/results.csv' OPTIONS (
  access_key_id = '<aws_access_key_id>',
  region = '<aws_region>',
  secret_access_key = '<aws_secret_access_key>'
);
```

Optionally, a credentials object can be created and used in place of providing
the service account key directly.

```sql
-- Create the credentials.
CREATE CREDENTIALS my_aws_creds PROVIDER aws OPTIONS (
  access_key_id = '<aws_access_key_id>',
  secret_access_key = '<aws_secret_access_key>',
);
-- And use them in copy public.users.
COPY public.users TO 's3://bucket/users.json' FORMAT json
CREDENTIALS my_aws_creds ( region '<aws_region>' );
```

### Copying files to the Delta table format

Queries can be copied to Delta tables by passing in an absolute path to a
blank directory (which will become the Delta table).

```shell
# Make a blank directory to receive the Delta table
mkdir your_new_delta_table
```

```sql
-- Copy the results of your query to Delta table format
COPY (SELECT 1) TO
'file:///Users/path/to/your_new_delta_table/'
FORMAT delta
```

When specifying the file path, make sure to prepend the path with `file://`.

Check out the video below for a more hands-on example:

<iframe width="560" height="315" src="https://www.youtube.com/embed/7W9Y_zZEENg?si=vNupX8HS8AnOrm_O" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
