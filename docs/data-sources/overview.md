---
layout: default
title: Connecting data sources
parent: Data sources
---

<!-- markdownlint-disable MD022 -->

<!-- prettier-ignore-start -->
# Connecting data sources
{: .no_toc }
<!-- prettier-ignore-end -->

<!-- markdownlint-enable MD022 -->

Connecting data sources can be done either through the dashboard, or through SQL
commands.

<!-- prettier-ignore -->
- TOC
{:toc}

## Connecting data sources using the dashboard

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

## Connecting data sources using SQL commands

Alternatively, data sources can be added using [CREATE EXTERNAL TABLE] or
[CREATE EXTERNAL DATABASE].

To add a **Postgres** data source using the [CREATE EXTERNAL DATABASE] command.

```sql
glare=> CREATE EXTERNAL DATABASE external_db
    FROM postgres
    OPTIONS (
        host = 'my.postgres.host',
        port = '5432',
        user = 'glaredb',
        password = 'password',
        database = 'glaredb_test',
    );
```

When we submit this command, validation is done to ensure we can properly
connect. Any errors connecting will be returned, for example:

```text
ERROR:  External database validation failed: Failed to connect to Postgres
instance: error connecting to server: Connection refused (os error 111)
```

If everything validates and no errors are returned, the data source is then
available to query from within the deployment.

[Data sources table]: /assets/images/data-sources-table.png
[Data sources dialog]: /assets/images/data-sources-dialog.png
[Postgres dialog]: /assets/images/postgres-dialog.png
[Postgres error]: /assets/images/postgres-error.png
[Postgres success]: /assets/images/postgres-success.png
[Postgres data source]: /docs/data-sources/supported/postgres
[CREATE EXTERNAL DATABASE]: /docs/sql-reference/sql-commands/create-external-database
[CREATE EXTERNAL TABLE]: /docs/sql-reference/sql-commands/create-external-table
