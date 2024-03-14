---
title: Storage
layout: home
nav_order: 6
has_children: true
---

## Storage

GlareDB is a compute-centered database engine, that separates storage
from compute. This separation enables a system that focuses
on connections between data in different forms and at lower and higher
levels of organization, and also provide a great deal of flexibility
and support.

While GlareDB is compute-centered, it has storage systems, and
supports a number of different storage formats and paradigms. This
multi-paradigm approach means that you can select the storage format
that makes the most sense for your data and your access patterns.
What's more, you can bring different storage formats to different parts
of your data as appropriate.

Even though GlareDB is compute-focused, understanding storage formats
and their impact on query performance and efficiency will help you in
designing powerful data infrastructure. 

Where transactional systems use indexes and data normalization to meet
performance targets, analytics systems take advantage of data layout and
data formats to meet performance goals. In virtually all systems,
there are trade-offs between storage compactness and query time, and
understanding these trade-offs will help you use GlareDB (and other
systems!) effectively.

### Formats: Columns and Records 

Internally, GlareDB uses the [Arrow] format to represent data, which
is an in-memory columnar format. Columnar formats are great because
they make operations over a single column or group of columns, like
sumarizations and averages, more efficient and they make it easier to
ignore columns that aren't relevant. 

Formats like [Parquet] and [Lance], as well as engines like [Delta]
and [Iceberg] that use Parquet, are also columnar. These columnar
storage formats are quite easy to translate into Arrow internally, and
store metadata in ways that make it possible to only read the required
segments of a file off of the disk.

Columnar formats have limitations: updates to a single record are
often scattered throughout a file which makes them particularly
expensive. Similarly, writing out columnar data may require
additional resources, or be inefficient if writes happen in very small
batches. For transactional workloads, columnar models make less sense. 

This table outlines some of the data formats and sources that GlareDB
supports and identifies the modality. [n.b. Engines like MySQL and
PostgreSQL have some multi-modality capability.]

| Format/System | Columnar | Record-Based |
|:--------------|:---------|:-------------|
| Parquet       | x        |              |
| Lance         | x        |              |
| Delta         | x        |              |
| Arrow         | x        |              |
| Avro          |          | x            |
| CSV           |          | x            |
| JSON          |          | x            |
| BSON          |          | x            |
| SQLite        |          | x            |
| MySQL         |          | x            |
| PostreSQL     |          | x            |
| Cassandra     | x        |              |
| Clickhouse    | x        |              |


-- TODO: write something about how columnar formats are written in some
   order, and being cognizant of the order that the data, so that you
   can use the order of the records in the parquet file as an index
   for ORDER BY and GROUP BY statements.

### Storage Engines and Encoding

- discuss MVCC and implications for GlareDB, 
- mention vacuuming requirements
- discuss encoding efficencies (protobufs and bson)

### Materialization: Roll Ups and Duplication

As software engineers, "duplication" is often 

- for data that doesnt change but is queried a lot it's ok to write
  it out a second time. (if the cost to run the query is more than the
  cost to write the data.)

### Considerations 

- access pattern
  - updates? what are the batch sizes of write operations
- data size
  - small and moderate datasets can safely be row-based.
- type system
  - every typesystem is a bit different, and sometimes this matters a
    lot.
- transactions/semantics



[Arrow]
