---
layout: default
title: CREATE TUNNEL
parent: SQL commands
---

# CREATE TUNNEL

Create an SSH Tunnel

## Syntax

```sql
CREATE TUNNEL <tunnel-name>
  FROM ssh
  OPTIONS (
    host = '<host>',
    port = '<port>',
    user = '<user>'
  );
```

| Field           | Description                               |
| --------------- | ----------------------------------------- |
| `<tunnel-name>` | A friendly name for the tunnel            |
| `<host>`        | The location of the SSH server            |
| `<port>`        | The port of the SSH server (default `22`) |
| `<user>`        | SSH user                                  |

## Examples

The following example creates a tunnel named `my_tunnel`, and uses it to connect
to a postgres data source.

```sql
CREATE TUNNEL my_tunnel
  FROM ssh
  OPTIONS (
    host = 'my.tunnel.host',
    port = '22',
    user = 'example_user'
  );

CREATE EXTERNAL DATABASE my_pg
    FROM postgres
    TUNNEL my_tunnel
    OPTIONS (
        host = 'my.postgres.host',
        port = '5432',
        user = 'glaredb',
        password = 'password',
        database = 'glaredb_test',
    );
```
