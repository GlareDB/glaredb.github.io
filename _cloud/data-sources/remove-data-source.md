---
layout: default
title: Remove a data source
parent: Managing data sources
nav_order: 4
---

# Remove a data source in GlareDB Cloud

The deployment overview page displays a table showing all data sources that are
currently connected to that deployment.

![Data sources table]

Removing a data source can be done by expanding the three dot context menu on a
data source. A menu will appear with a **Delete** option.

![Data sources menu]

Clicking delete will open a confirmation menu. Confirm the deletion to proceed,
or cancel.

![Data sources delete confirmation]

## SQL reference

If you prefer to use SQL for removing data sources, see the following SQL
reference:

- [DROP DATABASE]
- [DROP TABLE]

[Data sources table]: /assets/images/deployment-overview.png
[Data sources menu]: /assets/images/example_data_source_delete.png
[Data sources delete confirmation]: /assets/images/example_data_source_delete_confirm.png
[DROP DATABASE]: /glaredb/sql-commands/drop-database/
[DROP TABLE]: /glaredb/sql-commands/drop-table/
