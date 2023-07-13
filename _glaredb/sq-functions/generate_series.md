---
layout: default
title: generate_series
parent: SQL functions
---

# `generate_series`

Generate a series of integers.

Floats will be added in the next version.

## Syntax

```sql
generate_series(<start>, <stop> [, <step>])
```

| Field   | Description                           |
| ------- | ------------------------------------- |
| `start` | The integer to start generating from. |
| `stop`  | The integer to stop generating at.    |
| `step`  | The step size (defaults to 1).        |

## Examples

The following generates even numbers from 0 to 10.

```sql
select * from generate_series(0, 10, 2);
```
