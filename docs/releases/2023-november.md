---
layout: default
title: November 2023
parent: "Release notes"
nav_order: 4
---

# November 2023

## Table functions

**Available in**: [GlareDB@v0.6.1], [GlareDB Cloud]

- `read_excel` to read `.xlsx` files:

    ```sql
    select * from read_excel('file://data.xlsx')
    ```

## SQL improvements

**Available in**: [GlareDB@v0.6.1], [GlareDB Cloud]

- `DESCRIBE` supports describing tables

    ```sql
    DESCRIBE my_table
    ```

[GlareDB@v0.6.1]: https://github.com/GlareDB/glaredb/releases/tag/v0.6.1
[GlareDB Cloud]: https://console.glaredb.com
