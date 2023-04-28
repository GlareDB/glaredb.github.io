---
layout: default
title: DROP VIEW
parent: SQL commands
grand_parent: SQL reference
---

<!-- markdownlint-disable title-case-style -->

# DROP VIEW

<!-- markdownlint-enable title-case-style -->

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

[CREATE VIEW]: {{site.baseurl}}/docs/sql-commands/create-view
[system catalog]: {{site.baseurl}}/docs/system-catalog
