---
title: Join Across Data Sources with GlareDB and dbt
layout: default
nav_order: 3
parent: Tutorials
---

# Using dbt with GlareDB

GlareDB can serve as a destination warehouse for dbt, allowing you to build
transformation pipelines that work with data from multiple sources without
additional ETL infrastructure, so you can save money and time by not needing
to configure data extraction with tools like Fivetran or Stitch.
And since GlareDB can connect using the Postgres protocol, you can use the
existing Postgres adapter without needing anything new. This guide
will walk you through setting up and using dbt with GlareDB.

## Prerequisites

- dbt Core installed (`pip install dbt-postgres`)
- A GlareDB Cloud account (sign up at [console.glaredb.com])
- Basic familiarity with dbt concepts

## Setup

### 1. Initialize a dbt Project

Create a new dbt project:

```shell
dbt init my_glaredb_project
```

### 2. Configure dbt Credentials

Add your GlareDB credentials to your `profiles.yml` file. You can find your
connection details in GlareDB Cloud by clicking the "Connect" button and selecting
the Postgres tab.

```yaml
dbt_glaredb_quickstart:
  outputs:
    dev:
      dbname: org_name/deployment_name
      host: proxy.glaredb.com
      pass: your_password
      port: 6543
      schema: public
      threads: 1
      type: postgres
      user: your_username
  target: dev
```

> **Note**: When using your GlareDB Cloud connection string (which looks like
> `glaredb://user_name:password@org_name.proxy.glaredb.com:6543/deployment_name`),
> specify your `dbname` as `org_name/deployment_name` and the `host` as
> `proxy.glaredb.com`.

### 3. Test Your Connection

Verify your connection:

```shell
dbt debug
```

## Creating dbt Models

### Basic Model Example

First, define your sources in `models/properties.yml`:

```yaml
version: 2

sources:
  - name: glaredb
    schema: public
    database: default
    tables:
      - name: sales_data
```

Then, create a staging model in `models/staging_sales.sql`:

```sql
SELECT
    borough,
    neighborhood,
    building_class_category,
    residential_units,
    commercial_units,
    total_units,
    land_square_feet,
    gross_square_feet,
    year_built,
    sale_price,
    sale_date,
    latitude,
    longitude,
    bin,
    bbl
FROM {{ source('glaredb', 'sales_data') }}
```

### Working with Multiple Data Sources

GlareDB allows you to join data from different sources directly in your dbt
models. Here's an example that combines data from an external Postgres
data source in GlareDB and a remote file:

```sql
SELECT
    lookup.borough_name,
    sales.neighborhood,
    sales.building_class_category,
    sales.residential_units,
    sales.commercial_units,
    sales.total_units,
    sales.land_square_feet,
    sales.gross_square_feet,
    sales.year_built,
    sales.sale_price,
    sales.sale_date,
    sales.latitude,
    sales.longitude,
    sales.bin,
    sales.bbl
FROM {{ ref('staging_sales') }} sales
JOIN my_postgres.public.borough_lookup lookup
ON sales.borough = lookup.borough_id
```

If you won't be using your Postgres db for many queries, you may not
want to configure it as an external data source in GlareDB. In that case, you
could also write the previous model using the `read_postgres` function:

```sql
SELECT
    lookup.borough_name,
    sales.neighborhood,
    sales.building_class_category,
    sales.residential_units,
    sales.commercial_units,
    sales.total_units,
    sales.land_square_feet,
    sales.gross_square_feet,
    sales.year_built,
    sales.sale_price,
    sales.sale_date,
    sales.latitude,
    sales.longitude,
    sales.bin,
    sales.bbl
FROM {{ ref('staging_sales') }} AS sales
JOIN read_postgres(
    'postgres://demo:demo@pg.demo.glaredb.com/postgres',
    'public',
    'borough_lookup'
) AS lookup
ON sales.borough = lookup.borough_id
```

## Advanced Features

### Using Pre-hooks to Configure Data Sources

You can use dbt pre-hooks to make sure that any external databases are
set up before running your models:

```yaml
{{ config(
    materialized='view',
    pre_hook=[
    "CREATE EXTERNAL DATABASE IF NOT EXISTS my_postgres
    FROM postgres
    OPTIONS(
        connection_string = 'postgresql://user:pass@host:5432/dbname'
    );"
]
) }}
```

### File Upload Integration

GlareDB Cloud supports file uploads that can be referenced in your dbt models:

```sql
SELECT * FROM cloud_upload('myfile.xlsx')
```

### COPY TO Functionality

You can use GlareDB's COPY TO feature in post-hooks to export transformed data
to other destinations aside from your GlareDB warehouse:

```yaml
{{ config(
    materialized='view',
    post_hook=[
    "COPY public.my_model_name TO 's3://bucket/my_model_name.csv' FORMAT csv
    CREDENTIALS my_aws_creds ( region '<aws_region>' );"
]
) }}
```

## Best Practices

1. Use explicit schemas in your model references to avoid ambiguity when working
   with multiple data sources
2. Leverage dbt's documentation features to track data lineage across different
   sources
3. Consider using GlareDB's external database feature for frequently accessed data
   sources
4. Use pre-hooks to ensure data sources are properly configured before model
   execution

## Troubleshooting

Common issues and their solutions:

- **Connection Issues**: Ensure your connection string is properly formatted
  and includes the correct organization/deployment names
- **Performance**: Consider materializing intermediate models as tables for
  frequently accessed data

## Additional Resources

- [GlareDB Documentation]
- [dbt Documentation]
- [Sample dbt Project Repository]
- [Original blog post about GlareDB and dbt]

[console.glaredb.com]: https://console.glaredb.com
[GlareDB Documentation]: (https://docs.glaredb.com)
[dbt Documentation]: (https://docs.getdbt.com)
[Sample dbt Project Repository]: (https://github.com/GlareDB/dbt_glaredb_quickstart)
[Original blog post about GlareDB and dbt]: https://glaredb.com/blog/dbt-multiple-sources
