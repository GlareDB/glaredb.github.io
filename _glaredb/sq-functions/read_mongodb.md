---
layout: default
title: read_mongodb
parent: SQL functions
---

# `read_mongodb`

Read a MongoDB collection. The collection does not have to be a known data
source to GlareDB.

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
select * from read_mongodb(
  'protocol=mongodb+srv, user=mongo_user, password=mong_user_password',
  'my_mongo_database',
  'users'
);
```

Refer to the [documentation on MongoDB data sources] for more information.

[documentation on MongoDB data sources]: /docs/data-sources/supported/mongodb
