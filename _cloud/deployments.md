---
layout: default
title: Deployments
nav_order: 1
---

# Deployments

Deployments represent the persistent state of a GlareDB database.

Deployments inside an organization can be viewed from the main page, which can
be accessed any time by clicking the GlareDB logo in the top left of the
navigation.

![Deployments list]

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

You can delete a deployment from the **SQL workspace** page. Click the name of
the deployment in the navigation bar and from the menu, select **Delete**.

[Deployments list]: /assets/images/cloud/deployments/deployments-list.png
[Create deployment dialog]: /assets/images/cloud/deployments/create-deployment.png
