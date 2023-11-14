---
layout: default
title: GlareDB Node library
nav_order: 3
---

# GlareDB Node library

GlareDB can be used in [Node.js].

## Install

The `glaredb` module is available on npm <https://www.npmjs.com/package/@glaredb/glaredb>.
To install the module:

```shell
npm i @glaredb/glaredb
```

or if you're using `yarn`:

```shell
yarn add @glaredb/glaredb
```

## Usage

Import the `@glaredb/glaredb` module either using `require` (CommonJS) or
`import` (ESM). Then create a connection using `connect`.

```js
// CommonJS
const glaredb = require("@glaredb/glaredb");

const con = await glaredb.connect();
const res = await con.sql("SELECT 'hello JS'");
await res.show();

// ESM
import glaredb from "@glaredb/glaredb";

const con = await glaredb.connect();
const res = await con.sql("SELECT 'hello JS'");
await res.show();
```

By default, `connect` will use an in-memory database. A path may be provided to
`connect` to persist data after the script exits.

```js
import glaredb from "@glaredb/glaredb";

const con = await glaredb.connect("./my_db_path");
await con.sql("select * from persisted_table").show();
```

A GlareDB Cloud connection string may also be provided to `connect` to connect
to a Cloud deployment.

```js
import glaredb from "@glaredb/glaredb";

const str =
  "glaredb://<user>:<password>@<org>.remote.glaredb.com:6443/<deployment-name>";
const con = await glaredb.connect(str);
await con.sql("select * from cloud_table").show();
```

Connecting to a Cloud deployment via the [Node.js] library enables [Hybrid
execution] which allows queries to use the resources of both the remote
deployment and local machine.

### Querying data

GlareDB is able to query a variety of file types directly from [Node.js].

```js
import glaredb from "@glaredb/glaredb";

const con = await glaredb.connect();

// Query CSV files.
await con.sql("select * from './data.csv'").show();

// Query ndJSON files.
await con.sql("select * from './data.json'").show();

// Query Parquet files.
await con.sql("select * from './data.parquet'").show();
```

[Node.js]: https://nodejs.org/en
[Hybrid execution]: /glaredb/hybrid-execution
