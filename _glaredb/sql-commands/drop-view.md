---
layout: default
title: DROP VIEW
parent: SQL commands
---

# DROP VIEW

Drop a view. Note that builtin system views cannot be dropped. See [system
catalog] for an overview of builtin tables and views.

## Syntax

```sql
DROP VIEW [IF EXISTS] <view-name>;
```

| Field       | Description       |
| ----------- | ----------------- |
| `view-name` | The view to drop. |

`view-name` may optionally be qualified with a schema name.

## Examples

Drop a view named `my-view`. See [CREATE VIEW] for how to create a view.

```sql
DROP VIEW my-view;
```

[CREATE VIEW]: /docs/sql-reference/sql-commands/create-view.html
[system catalog]: /docs/sql-reference/system-catalog/
