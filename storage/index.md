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
| DuckDB        | x        |              |

To avoid needing to read every record to fulfill a query, record-based
systems use indexes to support more efficient queries. Indexes are
additional structures with compact representations that contain the
values of some column (or groups of columns), with pointers to each
row, that the query can use to limit the number records it must
inspect. Because indexes are stored in a particular order, queries can
also use the order of keys in an index to support sorts. While indexes
are possible for columnar formats in analytical workloads, as is the
case with Lance, they are less efficient given usage patterns and
system architectures.

For analytics engines, the encoding and organization of data has a big
impact on the data. While analytics engines lack indexes in most
cases, the _order_ of records in a columnar store can be used to avoid
expensive in-memory sorts, and support otherwise expensive filtering
operations. While you can run a query over data regardless of speed,
if you need to improve performance, or want to build a pipeline around
a query that's slow, you can try to write out or re-materialize the
out with a different field as the ordering constraint.

In all databases, query optimization is often about finding ways to
limit the amount of data to consider. In record based systems,
normalization (splitting logical records across tables,) and indexes
(materializing compact views) reduces the amount of data to
consider. For column based systems, saving additional copies of data
in different forms with different orderings, or that contain a subset
of fields, can have a huge impact on query performance.

<!-- TODO: connect to "use COPY TO to materialize different views of your data" -->

### Storage Engines and Encoding

GlareDB's data sources can be classified in a few groups:

- structured and semi-structured file formats. There are many
  different interchange formats, record encoding, and archival formats
  that allow us to write data to files, and share them between
  programs. JSON, Parquet, CSV, BSON, and Excel are just encoded raw
  data formats that GlareDB can interpret and present as a table. Each
  format has different properties and can provide different benefits
  to users. Some are easier to write and more widely supported as
  output formats, some are easier or more efficient to read
  programtiacally, and some are more transparent to read for humans.

- external database engines and services: GlareDB provides access to
  other database systems--like PostgreSQL, MySQL, MongoDB, SQLite,
  Snowflake and BigQuery, to enable joining data across data sources,
  or migrating data between formats and systems. Most of the time
  GlareDB is able to push operations _into_ the underlying database
  engine, which means these queries can take advantage of indexes in
  the underlying data and reduce the amount of data it needs to
  consider.

- storage engines, like Lance, DeltaLake and Iceberg, provide
  transactional and consistently properties that file formats cannot
  without the overhead of a process. At the same time, unlike extenral
  services and engines, these formats don't require a controling
  process and can work with all of the data stored to an object store
  like S3 or GCS. They do this by defining a protocol for writing and
  reading files that ensure that data is consistent and that writes
  are safe.

There are exceptions and edge cases: SQLite is somewhere between a
database and a file format, and the Parquet format has metadata that
makes it possible to push down some operations more like an external
database, while the implementations of Delta Lake are built upon
Parquet and JSON. However, this classification system may be useful
in understanding the limitations and features of a specific data
system.

### Materialization: Roll Ups and Duplication

For data sets that are changing often, having multiple copies of the
data can be very expensive: in addition to the extra space require,
you have to update many copies of the data any time the data changes,
and the coordination can become quite complex. However, for historic
data, or data that doesn't change after it's written, storing the data
in more than one form can support different queries, or save the data
in a grouped order or pre-compute and save various aggregates or sums
as needed. These saved roll ups are duplicated data, but because the
input data doesn't change, and the storage costs may be minimal, you
can save a lot of compute time by saving (or materializing) these
results. These kinds of transformations are always optimizations in
service of your use case.

When designing your data storage and infrastructure the key
considerations around what storage formats, engines or services, as
well as any kinds of transformation or materialization revolve around
considerations such as:

- how often will your application run  queries that access this data?

- how large is the input data set?

- how large is the output of these queries, typically?

- how often will the input data set change?

- are modifications to the input data, appending data to the "end," or
  are they modifications of existing records?

- what kind of application or system consumes the output?

- are there ordering requirements of the output? is the input ordering
  the same as the output ordering?

- what kind of data types does the input data have? does the
  storage format have a type system with the proper degree of
  fidelity?

Use the answers to these questions when selecting storage formats and
tools and designing your data infrastructure and application.
