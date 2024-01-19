---
layout: default
title: GlareDB Node.js library
nav_order: 3
---

# GlareDB Node.js library

GlareDB can be used in [Node.js].

For more information, refer to our in-depth [blog post Working with Node.js].

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

Provide a [connection string] to connect to [GlareDB Cloud].

```js
import glaredb from "@glaredb/glaredb";

const str =
  "glaredb://<user>:<password>@<org>.remote.glaredb.com:6443/<deployment-name>";
const con = await glaredb.connect(str);
await con.sql("select * from cloud_table").show();
```

Connecting to [GlareDB Cloud] with Node.js enables [Hybrid execution]. Queries
are optimized to use cloud and local compute resources. 

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
[blog post Working with Node.js]: https://glaredb.com/blog/node-bindings-announcement
[GlareDB Cloud]: https://console.glaredb.com
[connection string]: /glaredb/hybrid-execution/#getting-started-with-hybrid-execution
[Hybrid execution]: /glaredb/hybrid-execution
