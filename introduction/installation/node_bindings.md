---
title: Node Bindings
layout: default
nav_order: 3
parent: Installation
grand_parent: Getting Started
---

# Node.js Bindings

GlareDB binaries are distributed through npm, along with Node.js language
bindings. There are two ways to use GlareDB:

- **locally**, with optional disk persistence. In this scenario, queries are
  executed entirely in-process, and data exists in-memory or on-disk.

- **hybrid**, with [GlareDB Cloud]. In this scenario, queries are partitioned and
  optimized to run both in-process and using cloud compute. Data can be accessed
  and stored in cloud. When using [GlareDB Cloud], you can access your data
  in all of your applications.

**TypeScript** types are added by default, and so GlareDB can be used with
either JavaScript or TypeScript out of the box.

## Install

The `glaredb` module is available on npm
<https://www.npmjs.com/package/@glaredb/glaredb>. To install the module:

```shell
npm i @glaredb/glaredb
```

or, with `yarn`:

```shell
yarn add @glaredb/glaredb
```

After running `npm i @glaredb/glaredb`, the contents are added to
`node_modules/@glaredb`. There will be two subdirectories:

- `glaredb` - which contains language bindings and code that loads and runs
  the binary
- `glaredb-[platform]-[arch]` - this is a platform-specific GlareDB binary

## Usage

Import (ESM) or require (CJS) the `@glaredb/glaredb` module, then open a
connection using `connect`. Opening a connection starts, and interfaces with
the GlareDB binary.

```typescript
// ESM
import glaredb from "@glaredb/glaredb";

const con = await glaredb.connect();
const res = await con.sql("SELECT 'hello JS'");
await res.show();

// CommonJS
const glaredb = require("@glaredb/glaredb");

const con = await glaredb.connect();
const res = await con.sql("SELECT 'hello JS'");
await res.show();
```

### Local

When calling `connect` without any arguments, all data will exist in-memory and
will not persist once the process ends.

```typescript
const con = await glaredb.connect();
```

To persist data locally, specify a location as the first argument:

```typescript
const con = await glaredb.connect("./temp-dir");
```

### Hybrid with [GlareDB Cloud]

<!-- TODO: Link to Connection String doc -->

Provide a **connection string** to connect with [GlareDB Cloud].

```typescript
import glaredb from "@glaredb/glaredb";

const str = "glaredb://user:pass@org.glaredb.com:6443/deployment";
const con = await glaredb.connect(str);

const res = await con.sql("select * from cloud_table");
await res.show();
```

By connecting with [GlareDB Cloud], you can access _both_ local and cloud data.
For example, assuming you have a table in the cloud called `cloud_table`, and
a local JSON file called `report.json`:

```typescript
const res = await con.sql(`
SELECT * FROM cloud_table ct
JOIN './report.json' r ON ct.id = r.id;
`);
await res.show();
```

---

For more information, refer to our in-depth blog post [Working with Node.js].

[GlareDB Cloud]: https://console.glaredb.com
[Working with Node.js]: https://glaredb.com/blog/node-bindings-announcement
