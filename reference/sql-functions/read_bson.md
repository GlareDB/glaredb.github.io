---
layout: default
title: read_bson
parent: SQL functions
grand_parent: Reference
---

# `read_bson`

Reads one or more BSON files from the local filesystem or supported object store.

## Syntax

```sql
-- Location of the file or files:
read_bson(<url>);
-- Explicitly set the number of documents considered to infer the
-- schema (default is 100):
read_bson(<url>, schema_sample_size => 250);
```

Like other functions that produces table objects in queries,
`read_bson` works with all supported cloud providers for remote
storage: GCS, S3, Azure, and compatible APIs.

```sql
-- Using a cloud credentials object.
read_bson(<url>, <credential_object>);
-- Required named argument for S3 buckets.
read_bson(<url>, <credentials_object>, region => '<aws_region>');
-- Pass S3 credentials using named arguments.
read_bson(<url>, access_key_id => '<aws_access_key_id>', secret_access_key => '<aws_secret_access_key>', region => '<aws_region>');
-- Pass GCS credentials using named arguments.
read_bson(<url>, service_account_key => '<gcp_service_account_key>');
```

## Behavior

### Multiple Files

`read_bson` will expand glob patterns in the `<url>` argument and will
treat the resulting list of files as partitions of the same table.

### Schema Inference

By default, `read_bson`, sorts the files lexicographically and scans the
first 100 documents to infer the schema. Every field that appears is
added to the schema in the order that it appears as a nullable
field. The first type observed becomes the field's type.

After inferring a schema, the remaining data and files may be read
in any order.

The `schema_sample_size` option allows you to change the number of
documents considered when inferring the schema.
