---
layout: default
title: E-commerce
parent: Examples
nav_order: 1
---

# Multi-source data querying with GlareDB

## Scenario

GlobalMart is a leading e-commerce company operating in multiple countries. They
have been rapidly growing and expanding their product line, thus dealing with
increased volumes of data. They are a data-driven company and leverage their
data for providing better customer experiences, making key business decisions,
and predicting trends.

However, GlobalMart's data is distributed across different data storage systems
for various reasons:

1. **MongoDB**: They use MongoDB to store their customer data due to the
flexibility it offers in handling semi-structured data. It helps them quickly
evolve their data schema as their business grows and changes.

2. **Postgres**: They use a Postgres database to store transactional data. The
ACID properties of Postgres make it a great fit for reliably handling such
critical data.

3. **AWS S3**: They use S3 for storing unstructured data like customer reviews
in the form of JSON files. This allows for easy and cost-effective storage and
retrieval of large amounts of raw data.

4. **GCP**: They use the Google Cloud Platform for running their machine
learning models. The outputs, like next purchase predictions, are stored in CSV
files in a Google Cloud Storage bucket.

While each of these systems is great for the specific use cases they handle,
having data distributed like this poses a challenge for GlobalMart. Their
analysts, data scientists, and other stakeholders struggle to gain unified
insights from these disparate data sources.

They need a solution that allows them to query across all these data sources in
a unified manner, using the SQL language that their team is familiar with. This
is where GlareDB comes in. It allows creating external tables from different
data sources, making it possible to execute SQL queries across all these diverse
data storage systems. This solution will significantly streamline their data
analysis process and generate insights more effectively.

## Step 1: MongoDB - customer data

In MongoDB, you have a `customers` collection with documents structured as follows:

```json
{
  "_id": {
    "oid": "507f191e810c19729de860ea"
  },
  "first_name": "John",
  "last_name": "Doe",
  "email": "john.doe@example.com",
  "location": "United States",
  "membership_status": "premium",
  "signup_date": {
    "date": "2018-07-14T00:00:00Z"
  }
}
```

## Step 2: Postgres - transactional data

In your Postgres database, you have a `transactions` table
structured as follows:

```sql
CREATE TABLE transactions (
  transaction_id INT PRIMARY KEY,
  customer_id INT,
  product_id INT,
  purchase_date TIMESTAMP,
  amount DECIMAL(10, 2)
);
```

## Step 3: aws s3 - unstructured customer review data

On AWS S3, you store unstructured data in the form of
JSON files for customer reviews. Here's an example:

```json
{
  "review_id": "R1",
  "customer_id": "507f191e810c19729de860ea",
  "product_id": "P100",
  "review_date": "2022-05-14",
  "rating": 5,
  "comment": "Great product, fast delivery. Highly recommend!"
}
```

## Step 4: gcp - predictive analytics output

On Google Cloud Platform, you store CSV files that
represent the output from predictive models, such as
next purchase prediction:

```csv
customer_id,next_purchase_product_id,next_purchase_date
507f191e810c19729de860ea,P101,2023-02-01
```

## Step 5: creating external tables with our tool

With GlareDB, you can create external tables linked to
your diverse data sources.
Here's how you would define the tables for each source:

### MongoDB (customer data)

```sql
CREATE EXTERNAL TABLE customers
FROM mongodb
OPTIONS (
    connection_string = '<connection-string>',
    database = 'default',
    collection = 'customers'
);
```

### Postgres (transactional data)

```sql
CREATE EXTERNAL TABLE transactions
FROM postgres
OPTIONS (
    host = 'my.postgres.host',
    port = '5432',
    user = 'user',
    password = 'password',
    database = 'default',
    schema = 'public',
    table = 'transactions'
);
```

### AWS s3 (unstructured customer review data)

```sql
CREATE EXTERNAL TABLE reviews
FROM s3
OPTIONS (
    region = 'us-west-2',
    access_key_id = 'my_access_key_id',
    secret_access_key = 'my_secret_access_key',
    bucket = 'my_bucket',
    location = 'reviews/*.json'
);
```

### GCP (predictive analytics output)

```sql
CREATE EXTERNAL TABLE predictions
FROM gcs
OPTIONS (
    service_account_key = 'service-account-key',
    bucket = 'my_bucket',
    location = 'predictions/*.csv'
);
```

## Step 6: querying data with our tool

With GlareDB, users can run a query like the
following to get insights from multiple data sources:

```sql
SELECT
    c.first_name || ' ' || c.last_name as customer_name,
    t.product_id,
    t.purchase_date,
    r.rating,
    r.comment,
    p.next_purchase_product_id as next_id,
    p.next_purchase_date as next_date
FROM
    customers AS c
JOIN
    transactions AS t ON c.id::text = t.customer_id::text
JOIN
    reviews AS r ON c.id::text = r.customer_id::text
JOIN
    predictions AS p ON c.id::text = p.customer_id
WHERE
    c.location = 'United States'
    AND t.purchase_date > '2022-01-01'
    AND r.rating > 4
ORDER BY
    p.next_purchase_date;
```

This query retrieves information about high-rated
transactions by U.S. customers, and predicts their
next purchases.

```console
┌───────────────┬────────────┬─────────────────────┬────────┬─────────────────────────────────────────────────┬─────────┬────────────┐
│ customer_name │ product_id │ purchase_date       │ rating │ comment                                         │ next_id │ next_date  │
│ ──            │ ──         │ ──                  │ ──     │ ──                                              │ ──      │ ──         │
│ Utf8          │ Int32      │ Timestamp[µs, UTC]  │ Int32  │ Utf8                                            │ Utf8    │ Date32     │
╞═══════════════╪════════════╪═════════════════════╪════════╪═════════════════════════════════════════════════╪═════════╪════════════╡
│ John Doe      │ 100        │ 2022-01-01T10:10:10 │ 5      │ Great product, fast delivery. Highly recommend! │ P101    │ 2023-02-01 │
└───────────────┴────────────┴─────────────────────┴────────┴─────────────────────────────────────────────────┴─────────┴────────────┘
```

**Note:** These are simple examples and
real-world applications will have more
complex schemas and diverse data.
