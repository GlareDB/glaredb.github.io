---
layout: default
title: December 2023
parent: "Release notes"
nav_order: 5
---

## Lance Support

**Available in**: [GlareDB@v0.7.1], [GlareDB Cloud]
GlareDB now offers support for Lance.

Lance is a Modern columnar data format for ML and LLMs. Read more about Lance [here](https://lancedb.github.io/lance/).

```sql
SELECT * FROM lance_scan('path/to/file.lance');
```

## Documentation Improvements

**Available in**: [GlareDB@v0.7.1], [GlareDB Cloud]

We have made it easier to find the information you need, where you need it most.
Our functions catalog now contain 2 additional columns `description` and `example`.
These contain a short description of the function and an example of how to use it.

```sql
SELECT
  function_name,
  example,
  description
FROM glare_catalog.functions
```
