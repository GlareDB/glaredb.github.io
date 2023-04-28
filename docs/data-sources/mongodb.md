---
layout: default
title: MongoDB
parent: Data sources
---

# MongoDB

MongoDB is able to be used as an external data source. Either an entire cluster
or a single collection may be added as a data source.

{: .warning}

> The MongoDB data source is currently in preview. Features may be missing, and
> options are subject to change.


## External database

An entire MongoDB database can be added using the [CREATE EXTERNAL DATABASE]
command.

{: .important}

> There are two equivalent formats. In both formats, `database-name` will be the
> name of the database inside GlareDB. This cannot be qualified, and must be
> unique across all other databases in the deployment.

### External database long format

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

### External database long format options

| Field      | Description                                                                                         |
|------------|-----------------------------------------------------------------------------------------------------|
| `protocol` | The protocol to user. Either `mongodb` or `mongodb+srv`.                                            |
| `host`     | The host that the MongoDB service is available on.                                                  |
| `port`     | The port the MongoDB database is available on. Should only be specified if `protocol` is `mongodb`. |
| `user`     | A MongoDB database user.                                                                            |
| `password` | The password associated to the above `user`                                                         |

### External database compact format

```sql
CREATE EXTERNAL DATABASE <database-name>
  FROM mongo
  OPTIONS (
    connection_string = '<connection-string>',
  );
```

### External database compact format options

| Field               | Description                  |
|---------------------|------------------------------|
| `connection_string` | A MongoDB connection string. |

## External table

Adding an external table can be done through the [CREATE EXTERNAL TABLE]
command.

{: .important}

> There are two equivalent foramts. In both formats, `table-name` will be the
> name of the database inside GlareDB. `table-name` may optionally be qualified
> with a schema name.

### External table long format

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

#### External table long format options

| Field        | Description                                                                                         |
|--------------|-----------------------------------------------------------------------------------------------------|
| `protocol`   | The protocol to user. Either `mongodb` or `mongodb+srv`.                                            |
| `host`       | The host that the MongoDB service is available on.                                                  |
| `port`       | The port the MongoDB database is available on. Should only be specified if `protocol` is `mongodb`. |
| `user`       | A MongoDB database user.                                                                            |
| `password`   | The password associated to the above `user`                                                         |
| `database`   | The name of the database                                                                            |
| `collection` | The name of the collection                                                                          |

### External table compact format

```sql
CREATE EXTERNAL TABLE <table-name>
  FROM mongo
  OPTIONS (
    connection_string = '<connection-string>',
    database = '<database>',
    table = '<collection>',
  );
```

#### External table compact format options

| Field               | Description                                    |
|---------------------|------------------------------------------------|
| `connection_string` | Key value string containing connection details |
| `database`          | The name of the schema where the table resides |
| `collection`        | The name of the collection                     |

<!-- markdownlint-disable line-length -->

[CREATE EXTERNAL TABLE]: {{site.baseurl}}/docs/sql-commands/create-external-table
[CREATE EXTERNAL DATABASE]: {{site.baseurl}}/docs/sql-commands/create-external-database

<!-- markdownlint-enable line-length -->

