---
layout: default
title: read_excel
parent: SQL functions
---

# `read_excel`

Reads an Excel file from the local filesystem.

## Syntax

```sql
read_excel(<path>);
```

| Field        | Description                            |
| ------------ | -------------------------------------- |
| `path`       | Path to the Excel file                 |

## Examples

Read an Excel sheet named `sheet.xlsx` located in the current directory.

```sql
SELECT * FROM read_excel('./sheet.xlsx')
```
