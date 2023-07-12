---
layout: default
title: Deployments
nav_order: 1
---

# Deployments

Deployments represent the persistent state of a GlareDB database. Deployments
can be hooked up to a [Compute Engine] to power queries.

Deployments inside an organization can be viewed from the **Deployments** page.

![Org deployments]

## Creating deployments

Creating deployments can be done by clicking the **Create deployment** button.
Note the number of deployments that can be created is limited based on the
organization's billing plan. If the organization is at its limit, this button
will be disabled.

![Create deployment dialog]

## Deleting deployments

{: .warning}

> At this time, data from a deleted deployment can **never** be recovered. As
> we work towards a stable version, we will implement tiered deletion options.

Deleting a deployment can be done from the deployment's **Settings** page. From
the **Delete deployment** tab, you'll have the opportunity to delete a deployment.

![Delete deployment]

[Compute Engine]: /cloud/compute-engines
[Org deployments]: /assets/images/org-deployments.png
[Create deployment dialog]: /assets/images/create-deployment-dialog.png
[Delete deployment]: /assets/images/delete-deployment.png
