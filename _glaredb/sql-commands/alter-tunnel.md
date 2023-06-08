---
layout: default
title: ALTER TUNNEL
parent: SQL commands
---

# ALTER TUNNEL

Alter an SSH tunnel.

GlareDB currently only supports rotating keys using this command. For more
information on tunnels, see [Securing connections with SSH tunnels] and
[CREATE TUNNEL].

{: .important}

> After you rotate keys, don't forget to update your SSH server with the new
> public key.

## Syntax

```sql
ALTER TUNNEL [IF EXISTS] <tunnel-name> ROTATE KEYS;
```

| Field         | Description                  |
| ------------- | ---------------------------- |
| `tunnel-name` | Name of the tunnel to alter. |

## Examples

Creates a tunnel named `my_tunnel` then rotates its keys.

```sql
CREATE TUNNEL my_tunnel
  FROM ssh
  OPTIONS (
    host = 'my.tunnel.host',
    port = '22',
    user = 'example_user'
  );

ALTER TUNNEL my_tunnel ROTATE KEYS;
```

[Securing connections with SSH tunnels]: /docs/data-sources/overview.html#securing-connections-with-ssh-tunnels
[CREATE TUNNEL]: /docs/sql-reference/sql-commands/create-tunnel.html
