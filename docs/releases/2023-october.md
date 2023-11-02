---
layout: default
title: October 2023
parent: "Release notes"
nav_order: 3
---

# October 2023

## GlareDB Pro

**Available in**: [GlareDB Cloud]

Compute and storage at scale for all of your data applications. Only pay for
what you use: simple, powerful and flexible.

Read our announcement: [Introducing GlareDB Pro] or see our [Pricing page] for
more information.

Get started by:

- Signing up on <https://console.glaredb.com>
- Click **Upgrade** in the top right, or navigate to the billing page through
  Settings > Manage Plan

## PRQL support

**Available in**: [GlareDB@v0.6.0], [GlareDB Cloud]

```sql
-- SQL
set dialect = 'prql';
```

```python
# Python
con = glaredb.connect()
con.execute('set dialect = prql')
```

Read our article: [Adding PRQL Support to GlareDB]

## Local cloud storage

**Available in**: [GlareDB@v0.6.0]

GlareDB fully supports cloud storage using **GCS**, **S3**, **R2** and **MinIO** providers in Python and local CLI.

```shell
# Example for using S3 (and compatible stores) from CLI
glaredb \
  -l "s3://bucket/path" \
  -o access_key_id=key \
  -o secret_key_id=secret
```

## Misc updates and fixes

**Available in**: [GlareDB@v0.6.0]

- `\timing` command:

    ```shell
    > \timing
    Timing is on
    > select count(*) from lineitem;
    Time: 0.067s
    ```

- Run SQL from a file as a script:

    ```shell
    glaredb path/file.sql
    ```

**Available in**: [GlareDB@v0.6.0], [GlareDB Cloud]

- `DROP` operation is supported for temporary tables
- `CREATE OR REPLACE` support for native, temporary and external tables
- `IF NOT EXISTS` support for temporary tables

**Available in**: [GlareDB Python]

- `glaredb.Connection.sql()` now evaluates some operations eagerly.
- Polars [`LazyFrames`] support

[GlareDB Cloud]: https://console.glaredb.com/
[Introducing GlareDB Pro]: https://glaredb.com/blog/glaredb-pro-release-announcement
[Pricing page]: https://glaredb.com/pricing
[GlareDB@v0.6.0]: https://github.com/GlareDB/glaredb/releases/tag/v0.6.0
[Adding PRQL Support to GlareDB]: https://glaredb.com/blog/prql-announcement
[GlareDB Python]: https://pypi.org/project/glaredb/
[`LazyFrames`]: https://pola-rs.github.io/polars/py-polars/html/reference/lazyframe/index.html
