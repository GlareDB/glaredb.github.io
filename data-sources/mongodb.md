---
layout: default
title: MongoDB
parent: Data Sources
---

<!-- markdownlint-disable MD022 -->

<!-- prettier-ignore-start -->
# MongoDB
{: .no_toc }
<!-- prettier-ignore-end -->

<!-- markdownlint-enable MD022 -->

MongoDB is able to be used as an external data source. Either an entire cluster
or a single collection may be added as a data source.

<!-- prettier-ignore-start -->

- TOC
{:toc}
<!-- prettier-ignore-end -->

## Connect a MongoDB database

An entire MongoDB database can be added using the [CREATE EXTERNAL DATABASE]
command.

{: .important}

> There are two equivalent formats. In both formats, `database-name` will be the
> name of the database inside GlareDB. This cannot be qualified, and must be
> unique across all other databases in the deployment.

### Database long format

```sql
CREATE EXTERNAL DATABASE <database-name>
  FROM mongo
  OPTIONS (
    protocol = '<protocol>',
    host = '<host>',
    port = '<port>',
    user = '<user>',
    password = '<password>',
  );
```

### Database long format options

| Field      | Description                                                                                         |
| ---------- | --------------------------------------------------------------------------------------------------- |
| `protocol` | The protocol to user. Either `mongodb` or `mongodb+srv`.                                            |
| `host`     | The host that the MongoDB service is available on.                                                  |
| `port`     | The port the MongoDB database is available on. Should only be specified if `protocol` is `mongodb`. |
| `user`     | A MongoDB database user.                                                                            |
| `password` | The password associated to the above `user`                                                         |

### Database compact format

```sql
CREATE EXTERNAL DATABASE <database-name>
  FROM mongo
  OPTIONS (
    connection_string = '<connection-string>',
  );
```

### Database compact format options

| Field               | Description                  |
| ------------------- | ---------------------------- |
| `connection_string` | A MongoDB connection string. |

## Connect a single table

Adding an external table can be done through the [CREATE EXTERNAL TABLE]
command.

{: .important}

> There are two equivalent formats. In both formats, `table-name` will be the
> name of the database inside GlareDB. `table-name` may optionally be qualified
> with a schema name.

### Table long format

```sql
CREATE EXTERNAL TABLE <table-name>
  FROM mongo
  OPTIONS (
    protocol = '<protocol>',
    host = '<host>',
    port = '<port>',
    user = '<user>',
    password = '<password>',
    database = '<database>',
    collection = '<collection>',
  );
```

### Table long format options

| Field        | Description                                                                                         |
| ------------ | --------------------------------------------------------------------------------------------------- |
| `protocol`   | The protocol to user. Either `mongodb` or `mongodb+srv`.                                            |
| `host`       | The host that the MongoDB service is available on.                                                  |
| `port`       | The port the MongoDB database is available on. Should only be specified if `protocol` is `mongodb`. |
| `user`       | A MongoDB database user.                                                                            |
| `password`   | The password associated to the above `user`                                                         |
| `database`   | The name of the database                                                                            |
| `collection` | The name of the collection                                                                          |

### Table compact format

```sql
CREATE EXTERNAL TABLE <table-name>
  FROM mongo
  OPTIONS (
    connection_string = '<connection-string>',
    database = '<database>',
    collection = '<collection>',
  );
```

### Table compact format options

| Field               | Description                                    |
| ------------------- | ---------------------------------------------- |
| `connection_string` | Key value string containing connection details |
| `database`          | The name of the schema where the table resides |
| `collection`        | The name of the collection                     |

<!-- markdownlint-disable line-length -->

[CREATE EXTERNAL TABLE]: /reference/sql-commands/create-external-table
[CREATE EXTERNAL DATABASE]: /reference/sql-commands/create-external-database

<!-- markdownlint-enable line-length -->
