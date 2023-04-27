---
layout: default
title: CREATE VIEW
parent: SQL commands
---

<!-- markdownlint-disable title-case-style -->

# CREATE VIEW

<!-- markdownlint-enable title-case-style -->

Create a view.

## Syntax

```sql
CREATE [OR REPLACE] VIEW <view-name> AS <select-statement>;
```

| Field              | Description                               |
| ------------------ | ----------------------------------------- |
| `view-name`        | Name of the view.                         |
| `select-statement` | The select statement to use for the view. |

`view-name` may optionally be qualified with a schema.

If `OR REPLACE` is specified and a view with `view-name` already exists, the
view's definition will be replaced with the new `select-statement`.

## Examples

Create a view named `simple_select` that selects the value "1".

```sql
CREATE VIEW simple_select AS SELECT 1;
```
