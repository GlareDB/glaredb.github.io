---
title: Save Query Output
layout: default
nav_order: 2
parent: Tutorials
---

GlareDB provides a number of options to save the output of your queries,
including GlareDB tables, temp tables, and views, and external files in a
variety of formats.

## Creating a GlareDB Table from a File

For instance, say you have found a CSV file of user data on GitHub that you'd like
to save to our GlareDB instance. You can run:

```sql
CREATE TABLE my_user_data AS
SELECT * FROM read_csv(
    'https://github.com/GlareDB/glaredb/raw/main/testdata/csv/userdata1.csv'
);
```

to create a table from the CSV file.

<!--TODO: add link below -->
For more information, see the page on `CREATE TABLE`

## Creating a GlareDB View from a Query

Now, if you'd like to create an unmaterialized view of those users who have
comments in their record, you can do so with:

```sql
CREATE VIEW users_with_comments AS
SELECT * FROM my_user_data WHERE 
comments IS NOT NULL;
```

<!--TODO: add link below -->
For more information, see the page on `CREATE VIEW`

## Copying the Results of a Query to a File

### Copying to a local Excel File

Perhaps after running a query, you've found something noteworthy in the data
about users in the United States. Now you'd like to share the results with a
colleague who is great with Excel, but is not as comfortable with SQL. You can
run:

```sql
COPY
(SELECT * FROM my_user_data WHERE 'country' = 'United States')
TO './US_users.xlsx
```

This will save a copy of the data as an Excel file that you can share with your
colleagues. You can save the data in a variety of other formats, too, including
Parquet, CSV, and Delta.

### Copying to Cloud Storage

Instead of copying to a local file and then separately sharing with a
colleague, you can also copy the file directly to object storage on a cloud
provider. For instance, if you'd like to save the data to GCS, you can run:

```sql
COPY
(SELECT * FROM my_user_data WHERE 'country' = 'United States')
TO gcs OPTIONS (
    bucket = '<bucket>',
    location = 'file_location/US_users.xlsx',
    service_account_key = '<gcp_service_account_key>'
)
```

<!--TODO: add link below -->
You can copy data to files on GCS or S3. For more information, see the page on
`COPY TO`.

## Saving Queries and Exporting Data from GlareDB Cloud

The GlareDB SQL workspace makes it simple to take the results of a query and
either save them to a view or export them for local usage. After running a
query in Cloud, above the results of the query in the bottom part of the
screen, you can find buttons to `Export` or `Save query as view` - see
screenshot below.  

![Save query output from GlareDB Cloud]

<!--TODO: add link below -->
For more information, see the page on working with the GlareDB SQL workspace.

[Save query output from GlareDB Cloud]: /assets/images/tutorials/saving-queries-and-exporting-data-from-glaredb-cloud.png
