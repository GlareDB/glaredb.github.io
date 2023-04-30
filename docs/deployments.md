---
layout: default
title: Deployments
nav_order: 2
---

# Deployments

Deployments are the basic unit of compute in GlareDB and are responsible for
executing SQL queries and accessing data sources.

Deployments inside an organization can be view from the **Deployments** page.

![Org deployments]

## Dedicated vs Serverless

Deployments come in two variants: dedicated and serverless.

**Dedicated** deployments are isolated from other tenants, and resource sizing
can be configured to best fit the workload being run. Dedicated deployments are
only available on a paid plan.

**Serverless** deployments run all workloads on a shared set of compute nodes.
Resources are not guaranteed, and performance can flucuate depending on
activity. Serverless deployments are available on free and paid plans.

## Creating deployments

Creating deployments can be done by clicking the **Create deployment** button.
Note the number of deployments that can be created is limited based on the
organization's billing plan. If the organization is at its limit, this button
will be disabled.

![Create deployment dialog]

## Deleting deployments

Deleting a deployment can be done from the deployment's **Settings** page. From
the **Delete deployment** tab, you'll have the opportunity to delete a deployment.

![Delete deployment]

[Org deployments]: /assets/images/org-deployments.png
[Create deployment dialog]: /assets/images/create-deployment-dialog.png
[Delete deployment]: /assets/images/delete-deployment.png
