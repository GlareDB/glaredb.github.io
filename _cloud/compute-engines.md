---
layout: default
title: Compute engines
nav_order: 2
---

# Compute engines

Compute engines are virtual machines responsible for executing SQL queries and
accessing data sources.

All GlareDB [Deployments] can access the default serverless compute engine, which
is available in our [Free Tier].

Compute engines inside an organization can be viewed from the **Compute Engines**
page.

![Org compute engines]

## Create compute engines

Creating compute engines can be done by clicking the **Add engine** button. Note
that this feature is only available for paid plans.

![Create engine dialog]

Created engines are by default stopped. To use the engine, turn it on from the 3
dot menu.

![Start engine]

[Deployments]: /cloud/deployments
[Free Tier]: /docs/about/free-tier
[Org compute engines]: /assets/images/compute-engines.png
[Create engine dialog]: /assets/images/create-engine-dialog.png
[Start engine]: /assets/images/compute-engine-start.png
