---
layout: default
title: COPY TO
parent: SQL commands
---

# COPY TO

Copy a query result to a file.

GlareDB currently only supports creating local copies using this command.

## Syntax

```sql
COPY (<query>) TO LOCAL [FORMAT <format>] (location <path>);
```

| Field    | Description                                                       |
| -------- | ----------------------------------------------------------------- |
| `query`  | The query to execute, of which the results will be copied.        |
| `format` | Output format. One of **csv** (default), **json** or **parquet**. |
| `path`   | Path where the results will be copied.                            |

## Examples

Copy a query, `select 1`, to a file `result.parquet` in the current working
directory.

```sql
copy (select 1) to local format parquet (location 'result.parquet');
```
