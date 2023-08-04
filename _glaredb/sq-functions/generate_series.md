---
layout: default
title: generate_series
parent: SQL functions
---

# `generate_series`

Generate a series of integers or decimals.

## Syntax

```sql
generate_series(<start>, <stop> [, <step>])
```

| Field   | Description                                    |
| ------- | ---------------------------------------------- |
| `start` | The integer or decimals to start generating from. |
| `stop`  | The integer or decimals to stop generating at.    |
| `step`  | The step size (defaults to 1).                 |

## Examples

The following generates even numbers from 0 to 10.

```sql
select * from generate_series(0, 10, 2);
```

The following generates decimals from 0.0 to 1.0, stepping by 0.1:

```sql
select * from generate_series(0, 1, 0.1);
```
