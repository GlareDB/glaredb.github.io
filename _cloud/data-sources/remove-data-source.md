---
layout: default
title: Remove a data source
parent: Managing data sources
nav_order: 4
---

# Remove a data source in GlareDB Cloud

The **Schema Explorer** in the **SQL workspace** shows every data source that's
connected to your deployment.

To disconnect an external database (such as MongoDB, MySQL, Postgres or
Snowflake), run the [DROP DATABASE] SQL command.

To remove an external table (such as a file in GCS or S3 cloud storage), run the
[DROP TABLE] SQL command.

![drop database sql workspace]

![drop database result]

[DROP DATABASE]: /glaredb/sql-commands/drop-database/
[drop database sql workspace]: /assets/images/cloud/data-sources/drop-database.png
[drop database result]: /assets/images/cloud/data-sources/drop-database-result.png
[DROP TABLE]: /glaredb/sql-commands/drop-table/
