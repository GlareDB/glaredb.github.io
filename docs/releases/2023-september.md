---
layout: default
title: September 2023
parent: "Release notes"
nav_order: 2
---

# September 2023

## Hybrid Execution

**Available in**: [GlareDB@v0.5.0], [GlareDB Cloud]

Read our announcement: [Hybrid Execution: Scale your workflow with GlareDB Cloud].

Utilize the power of cloud alongside your local machine to query data wherever
it resides. You can `SELECT` and `JOIN` _local_ data with all of the data in
your cloud deployment. Query execution is optimized so that processing takes
place both locally and remotely to minimize transport related overhead. You can
use Hybrid Execution in both the **GlareDB CLI** and [GlareDB Python library].

Get started by:

- Signing up on <https://console.glaredb.com>
- Click **Connect**
- Follow the instructions to connect locally with the GlareDB CLI or in Python

## SQL workspace improvements

**Available in**: [GlareDB Cloud]

- The SQL workspace now contains command completion and hints for tables and
  table functions
- The stability of the SQL workspace was drastically improved
- Database users and SSH tunnels were added to the sidebar
- A manual refresh button was added to the schema explorer

## Inferred table functions

**Available in**: [GlareDB@v0.5.0], [GlareDB Cloud]

Table functions can now be inferred from files. Previously, to scan a CSV file
you'd have to call `csv_scan(...)`. Now, you can simply just query the file
directly:

```sql
SELECT * FROM './customer_report.csv';
```

This works for remote files as well (try out the below query!):

```sql
SELECT * FROM
  'https://huggingface.co/datasets/fka/awesome-chatgpt-prompts/raw/main/prompts.csv'
LIMIT 10;
```

Note that you will still need to use `csv_scan` where credentials need to be
passed.

## CLI completion history and hints

**Available in**: [GlareDB@v0.5.0]

- You can now re-run multi-line commands - simply press ⬆️ to cycle through
  previously run commands.
- The CLI now has improved command-completion hints using session history
- You can now exit the CLI with `exit` or `\q`, in addition to `CTRL-d`

## Dashboard design

**Available in**: [GlareDB Cloud]

The entirety of the [GlareDB Cloud] dashboard was redesigned with simpler
navigation and views in mind. There are now three main pages:

- The SQL workspace
- The deployment list page (available by clicking the top-left GlareDB logo)
- The unified settings page (available from the user dropdown > Settings)

In addition, we've improved the dialog for connecting a data source. You can now
add an SSH Tunnel within the form, as well as retry failed connections. We also
show you the exact SQL and output that's running.

## Additional BigQuery type support

**Available in**: [GlareDB@v0.5.0], [GlareDB Cloud]

- We now support Array, Record, Struct and Big Numeric types for BigQuery data
  sources

## Misc updates and fixes

**Available in**: [GlareDB@v0.5.0], [GlareDB Cloud]

- `list_columns(<database>, <schema>, <table>)` table function was added
- The GlareDB Python library can now be installed in Microsoft Fabric

[GlareDB@v0.5.0]: https://github.com/GlareDB/glaredb/releases/tag/v0.5.0
[GlareDB Cloud]: https://console.glaredb.com/
[Hybrid Execution: Scale your workflow with GlareDB Cloud]: https://glaredb.com/blog/hybrid-execution
[GlareDB Python library]: https://pypi.org/project/glaredb/
