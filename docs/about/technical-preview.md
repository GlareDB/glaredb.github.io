---
title: Technical preview
layout: default
parent: What is GlareDB?
nav_order: 4
---

# Technical preview

{: .important}

> GlareDB is currently in the `0.X.Y` version ranges. With feedback from the
> technical preview phase, we're working towards a stable version with core
> feature completeness and additional Postgres compatibility.

GlareDB started with a Limited Preview started in December, 2022, and was made
available to a small number of select users and friends.

On May 1st, 2023, GlareDB moved into Technical Preview, and became available to
a wider audience with early access codes.

On May 11, 2023, the Technical Preview became generally available. It is
available to everyone with a free tier to get started.

On May 26, 2023, [github.com/GlareDB/glaredb] was made open source. See our
[open source announcement] for more information.

On July 12, 2023, GlareDB moved from `0.0.X` ranges to `0.2.0`, marking a
significant milestone towards technical stability with a growing feature set.

## Stability

{: .important}

> While GlareDB is in technical preview, complete stability cannot be
> guaranteed.

## Missing features

In the current state, the application is missing a few core features that are
necessary to move towards a stable version range.

1. Postgres compatibility

   In order to achieve a stable version range, we are dedicated to ensuring that
   the tools and functions that work with Postgres, work with GlareDB. If
   there's a tool in your stack that's not working as expected with GlareDB,
   we'd love to hear about it.

1. SSH connections

   In order to support more architectures, we are working on increasing our support
   for connecting to data sources through ssh tunnels. Currently, SSH support
   exists for MySQL and Postgres.

1. Regional support

   Supported regions are limited while in technical preview. Users from anywhere
   may try GlareDB, but may experience latency. To work around this,
   [try running GlareDB locally].

[github.com/GlareDB/glaredb]: https://github.com/GlareDB/glaredb
[open source announcement]: https://glaredb.com/blog/glaredb-goes-open-source
[try running GlareDB locally]: /glaredb/local
