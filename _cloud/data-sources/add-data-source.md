---
layout: default
title: Add a data source
parent: Managing data sources
---

# Add a data source in GlareDB Cloud

The deployment overview page displays a table showing all data sources that are
currently connected to that deployment. Adding a new data source can be done by
clicking the **Add data source** button.

![Data sources table]

A new dialog will pop up showing all supported data sources.

![Data sources dialog]

Clicking one of the data source types will take you to the next screen where you
will need to provide details on how to connect.

![Postgres dialog]

In our example, we picked **Postgres**. We are then asked to provide a **Name**,
**Host**, **Port**, **Database**, **User**, and **Password**. (See [Postgres
data source] for more information on these fields.)

Submitting this form will validate the connection. If there's an issue with
connecting, an error message will be displayed.

![Postgres error]

If everything succeeds, a confirmation message will be displayed, and the data
source is now able to be queried from within your deployment.

![Postgres success]

## SQL reference

If you prefer to use SQL for adding data sources, see the following SQL
reference:

- [CREATE EXTERNAL DATABASE]
- [CREATE EXTERNAL TABLE]

[Data sources table]: /assets/images/data-sources-table.png
[Data sources dialog]: /assets/images/data-sources-dialog.png
[Postgres dialog]: /assets/images/postgres-dialog.png
[Postgres error]: /assets/images/postgres-error.png
[Postgres success]: /assets/images/postgres-success.png
[Postgres data source]: /docs/data-sources/supported/postgres
[CREATE EXTERNAL DATABASE]: /glaredb/sql-commands/create-external-database
[CREATE EXTERNAL TABLE]: /glaredb/sql-commands/create-external-table
