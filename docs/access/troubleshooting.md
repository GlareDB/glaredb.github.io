---
layout: default
title: Troubleshooting
parent: Access deployments
---

# Troubleshooting connections

Common errors and how to fix them. Can't find your issue here? Reach out to us
at [support@glaredb.com].

## "Missing org id"

We route connections to the correct deployment with the help of the
organization. By default, we display a connection string with a hostname that
includes the organization name. However, this requires that the client you're
using properly supports SNI (Server Name Indication).

If you get an error like the following, it's likely that your client does not
support SNI:

```
missing org ID: pass it as an option, or subdomain in proxy or in database as '<org>/<db>'
```

To work arround this, we also accept connection strings in this form:

```
postgresql://<user>:<password>@proxy.glaredb.com:6543/<org-name>/<deployment-name>
```

The main difference here the organization name being provided as part of the
database name.

For example, a deployment named "my_deployment" inside an organization named
"my_org" would be formatted like so:

```
postgresql://<user>:<password>@proxy.glaredb.com:6543/my_org/my_deployment
```

[support@glaredb.com]: mailto:support@glaredb.com
