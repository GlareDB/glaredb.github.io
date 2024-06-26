---
title: Deployments
layout: default
nav_order: 1
parent: GlareDB Cloud
---

# Deployments

A deployment is a fully-managed, logical instance of GlareDB. With a
[GlareDB Cloud] deployment, you can access your data locally, in notebooks, and
in applications.

Deployments inside an organization can be viewed from the main page, which can
be accessed any time by clicking the GlareDB logo in the top left of the
navigation.

![deployment list]

## Creating deployments

Creating deployments can be done by clicking the **Create deployment** button.
Note: the number of deployments that can be created is limited based on the
[organization’s billing plan]. If the organization is at its limit, this button
will be disabled.

## Connecting to deployments

Connection details for a deployment can be accessed from the SQL workspace by
clicking the **Connect** button.

![Connect]

### About connection strings

[CLI], [Python], and [Node.js] connection strings utilize the `glaredb://`
protocol. When connecting through the `glaredb://` protocol, all queries are
executed in a hybrid manner. It is recommended to connect through this protocol
when working locally, in notebooks or in officially supported language bindings.

GlareDB also supports the `postgresql://` protocol. Simply click the `Postgres`
tab of the connection dialog and copy the connection string. When connecting
through the `postgresql://` protocol, all execution occurs remotely. It is
recommended to connect through this protocol where needed such as in
languages that do not yet have officially supported bindings or `psql` and
other Postgres clients.

## Generating new passwords

A new username and password combo can be generated by clicking the
**New password** button. A randomly generated username and password will be
displayed. The password will only be displayed once.

![password]

{: .important}

> Password are only ever shown once. Store your password somewhere secure, as it
> can never be retrieved again. In cases where you forget your password, you can
> generate a new one.

## Deleting passwords

Credentials for the deployment are listed in the **Database users panel**,
located from the sidebar of the **SQL workspace**. To delete a credential, click
the three dot menu and select **Remove**.

![manage passwords]

## Deleting deployments

{: .warning}

> At this time, data from a deleted deployment can never be recovered. As we work
> towards v1, we will implement tiered deletion options.

You can delete a deployment from the SQL workspace page. Click the name of the
deployment in the navigation bar and from the menu, select Delete.

[GlareDB Cloud]: https://console.glaredb.com
[deployment list]: /assets/images/cloud/deployments/deployment-list.png
[organization’s billing plan]: /cloud/billing.html
[Connect]: /assets/images/cloud/deployments/connect-button.png
[CLI]: /introduction/installation/locally-cli.html
[Python]: /introduction/installation/python-bindings.html
[Node.js]: /introduction/installation/node_bindings.html
[password]: /assets/images/cloud/deployments/new-password.png
[manage passwords]: /assets/images/cloud/deployments/manage-passwords.png
