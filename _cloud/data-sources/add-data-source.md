---
layout: default
title: Add a data source
parent: Managing data sources
nav_order: 1
---

# Add a data source in GlareDB Cloud

The main page displays all of your deployments with a summary count of each
data source. To add a new data source, click the **+** button.

![Add data source button]

You can also add a data source from the **SQL workspace** page by clicking
**+ Connect data source** in the navigation bar at the top of the page.

A new dialog will pop up showing all supported data sources.

![Data sources dialog]

After selecting one of the supported data source types, you will see a form:

![Add pg data source]

Submitting this form will:

- validate that a connection can be made with the data source
- if valid, save this data source as a database in your GlareDB deployment

The exact SQL being run and its output (including errors) are displayed.

![Add pg data source output]

![Add pg data source output error]

## SQL reference

If you prefer to use SQL for adding data sources, see the following SQL
reference:

- [CREATE EXTERNAL DATABASE]
- [CREATE EXTERNAL TABLE]

[Add data source button]: /assets/images/cloud/data-sources/add-datasource-button.png
[Data sources dialog]: /assets/images/cloud/data-sources/data-sources-dialog.png
[Add pg data source]: /assets/images/cloud/data-sources/add-pg-data-source.png
[Add pg data source output]: /assets/images/cloud/data-sources/add-pg-data-source-output.png
[Add pg data source output error]: /assets/images/cloud/data-sources/add-pg-data-source-output-error.png
[CREATE EXTERNAL DATABASE]: /glaredb/sql-commands/create-external-database/
[CREATE EXTERNAL TABLE]: /glaredb/sql-commands/create-external-table/
