---
layout: default
title: Transactions
parent: SQL reference
---

# Transactions

GlareDB does not currently have complete transaction support.

## Command behavior

This section describes the current behavior of transaction related commands in
GlareDB.

<!-- markdownlint-disable title-case-style -->

### BEGIN, COMMIT, and ROLLBACK

<!-- markdownlint-enable title-case-style -->

`BEGIN`, `COMMIT`, and `ROLLBACK` currently lack transactional semantics.
Commands submitted after calling `BEGIN` will have their effects immediately
observable to all other clients connected to the deployment. A `ROLLBACK` will
not rollback changes that have been made within the transaction.

For example, if client 'A' executes `BEGIN; CREATE SCHEMA my_schema;`, client
'B' will be able to see the schema `my_schema` even though client 'A' did not
commit this change. If client 'A' executes `ROLLBACK`, the schema `my_schema`
will _not_ be removed from the system.

<!-- markdownlint-disable title-case-style -->

### SHOW TRANSACTION ISOLATION LEVEL

<!-- markdownlint-enable title-case-style -->

`SHOW TRANSACTION ISOLATION LEVEL` will return "read uncommitted".

## Future support

GlareDB will support transactional consistency for DDL (`CREATE EXTERNAL
DATABASE`, etc) commands in the future, alongside supporting transactional
consistency for DML commands (`SELECT`, etc) for some data sources.
