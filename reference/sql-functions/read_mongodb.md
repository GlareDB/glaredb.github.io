---
layout: default
title: read_mongodb
parent: SQL functions
grand_parent: Reference
---

# `read_mongodb`

Read data from an arbitrary MongoDB collection. The collection does
not have to be a known data source to GlareDB.

If you have multiple collections in one MongoDB deployment or are
regularly using the same MongoDB data source, consider [setting up a
MongoDB data source](/docs/data-sources/supported/mongodb).

## Syntax

```sql
read_mongodb(<connection_str>, <database>, <collection>)
```

| Field            | Description                  |
| ---------------- | ---------------------------- |
| `connection_str` | A MongoDB connection string. |
| `database`       | The name of the database.    |
| `collection`     | The name of the collection.  |

## Examples

In the following example, a 'users' collection is queryed.

```sql
SELECT mdb.* FROM read_mongodb(
  'protocol=mongodb+srv, user=mdb_user, password=mdb_user_password',
  'mdbDatabaseName',
  'collectionName'
) AS mdb;
```

This exposes the fields from the MongoDB collection as a collection of
fields with the `mdb.` prefix in a SQL query. Select an alternate
prefix, or no prefix as you see fit.

## Behavior

GlareDB samples up to 100 documents from the MongoDB collection, or
less for smaller collections, building a schema that has the sum of
all fields in the observed documents. Follow [this
issue](https://github.com/GlareDB/glaredb/issues/2144) for discussion
of changes to schema inference for MongoDB data sources.
