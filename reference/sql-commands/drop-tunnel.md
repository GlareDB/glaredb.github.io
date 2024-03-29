---
layout: default
title: DROP TUNNEL
parent: SQL commands
grand_parent: Reference
---

# DROP TUNNEL

Drop a tunnel.

## Syntax

```sql
DROP TUNNEL [IF EXISTS] <tunnel-name>;
```

| Field         | Description         |
| ------------- | ------------------- |
| `tunnel-name` | The tunnel to drop. |

## Examples

Drop a tunnel named `my_tunnel`. See [CREATE TUNNEL] for how to create a
tunnel.

```sql
DROP TUNNEL my_tunnel;
```

[CREATE TUNNEL]: /reference/sql-commands/create-tunnel/
