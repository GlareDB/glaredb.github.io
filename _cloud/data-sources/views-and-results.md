---
layout: default
title: Saving your queries and results
parent: Managing data sources
nav_order: 3
---

# Save a query

Have a complicated query, such as joining multiple data sources? The SQL
workspaces offers two easy-to-use features: views and exporting results.

## Save queries as views

To save the current query in the SQL workspace editor as a view, simply click
the **Save view** button at the top right of the editor. You must select a
schema and a name for the view.

![Save as view]

If you want to use a schema other than `public`, then simply create a new schema
in GlareDB. For more information, refer to [CREATE SCHEMA].

## Export results

To export results from the SQL workspace editor, first run a query. Then, click
**Export** in the top right of the results table. From there, select how you
want to save your results.

![Export results]

[Save as view]: /assets/images/sql_workspace_view.png
[CREATE SCHEMA]: /glaredb/sql-commands/create-schema/
[Export results]: /assets/images/sql_workspace_export.png
