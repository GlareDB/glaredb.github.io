---
title: Technical preview
layout: default
parent: What is GlareDB?
nav_order: 4
---

# Technical preview

{: .important}

> GlareDB is currently in the version 0.0.X ranges. With feedback from the
> technical preview phase, we're working towards a stable version with core
> feature completeness and additional Postgres compatibility.

GlareDB started with a Limited Preview started in December, 2022, and was made
available to a small number of select users and friends.

On May 1st, 2023, GlareDB moved into Technical Preview, and became available to
a wider audience with early access codes.

On May 11, 2023, the Technical Preview became generally available. It is
available to everyone with a free tier to get started.

On May 26, 2023, [github.com/GlareDB/glaredb] was made open source.

## Stability

{: .important}

> While GlareDB is in technical preview, complete stability cannot be
> guaranteed.

## Deployment updates

While in technical preview, GlareDB deployments are updated as follows:

1. **Serverless** - updated live as we cut new releases.

1. **Dedicated** - only updated if you manually restart them.

{: .important}

> To reach a stable version, we are committed to improving the update experience
> with opt-in controls and backwards compatibility.

### Restarting a dedicated deployment

Navigate to the deployment and click **Stop deployment** in the top right.

![stop deployment]

Once the deployment successfully stops, start it again by clicking
**Start deployment**.

![start deployment]

## Missing features

In the current state, the application is missing a few core features that are
necessary to move towards a stable version range.

1. Postgres compatibility

   In order to achieve a stable version range, we are dedicated to ensuring that
   the tools and functions that work with Postgres, work with GlareDB. If
   there's a tool in your stack that's not working as expected with GlareDB,
   we'd love to hear about it.

2. SSH connections

   In order to support more architectures, we are working on support for
   connecting to data sources through ssh tunnels.

   **Update**: as of `v0.0.25` we now support SSH tunnels for MySQL and Postgres.

3. Regional support

   Supported regions are limited while in technical preview. Users from anywhere
   may try GlareDB, but may experience latency.

[github.com/GlareDB/glaredb]: https://github.com/GlareDB/glaredb
[stop deployment]: /assets/images/dedicated-stop.png
[start deployment]: /assets/images/dedicated-start.png
