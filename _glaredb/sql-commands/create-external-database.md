---
layout: default
title: CREATE EXTERNAL DATABASE
parent: SQL commands
---

# CREATE EXTERNAL DATABASE

Use an external database as a data source in GlareDB. See [Data sources] to
learn more.

## Syntax

```sql
CREATE EXTERNAL DATABASE <database-name>
    FROM <data-source-type>
    [TUNNEL <tunnel-name>]
    OPTIONS (<data-source-options>);
```

| Field                 | Description                                      |
| --------------------- | ------------------------------------------------ |
| `database-name`       | Name of the database as it appears in GlareDB.   |
| `data-source-type`    | The type of data source, for example `postgres`. |
| `tunnel-name`         | [SSH tunnel] to connect with.                    |
| `data-source-options` | Options specific to this data source type.       |

Note that `database-name` must be unique within a GlareDB deployment.

## Examples

Create an external database named `external_db` using a Postgres data source.

```sql
CREATE EXTERNAL DATABASE external_db
    FROM postgres
    OPTIONS (
        host = 'my.postgres.host',
        port = '5432',
        user = 'glaredb',
        password = 'password',
        database = 'glaredb_test',
    );
```

[Data sources]: /docs/data-sources
[SSH tunnel]: /docs/data-sources/overview.html#securing-connections-with-ssh-tunnels
