---
layout: default
title: Data types
parent: SQL reference
---

# Data types

GlareDB uses many [DataFusion] components under the hood, including much of its type
system. Internally, all values are represented using Arrow. This section
provides a mapping between SQL types and Arrow types.

| SQL type                  | Arrow type                   |
|---------------------------|------------------------------|
| BOOLEAN                   | Boolean                      |
| TINYINT                   | Int8                         |
| SMALLINT                  | Int16                        |
| INT                       | Int32                        |
| BIGINT                    | Int64                        |
| FLOAT, REAL               | Float32                      |
| DOUBLE                    | Float64                      |
| DECIMAL(precision, scale) | Decimal128(precision, scale) |
| DATE                      | Date32                       |
| TIME                      | Time64                       |
| TIMESTAMP                 | Timestamp                    |
| INTERVAL                  | Interval                     |
| BYTEA                     | Binary                       |
| TEXT, STRING              | Utf8                         |
| ARRAY                     | List                         |

The `arrow_typeof` function can be used to determine the arrow type used for a
given SQL expression.

``` sql
glaredb=> select arrow_typeof(1);
 arrowtypeof(Int64(1))
-----------------------
 Int64
(1 row)

glaredb=> select arrow_typeof('11-12-23'::date);
 arrowtypeof(Utf8("11-12-23"))
-------------------------------
 Date32
(1 row)
```

[DataFusion]: https://arrow.apache.org/datafusion/user-guide/introduction.html
