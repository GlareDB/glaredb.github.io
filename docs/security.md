---
layout: default
title: Security
nav_order: 7
---

# Security

GlareDB is committed to keeping customer data safe and building trust with our
users.

## What data does GlareDB store?

GlareDB stores information required to access your databases and services, which
may include items such as host names, usernames, and passwords. This data is
encrypted at rest, and is completely isolated from other tenants within GlareDB.

During query execution, GlareDB will attempt to pull in data from connected data
sources in order to execute the query using these credentials. This data is only
stored for the lifetime of the query, and is removed immediately following the
completion of the query.

Intermediate results during a query may be written out to disk to accommodate
larger than memory queries, and are automatically removed following completion
of the query. Intermediate results are never commingled with other running
queries.

## Who can access my data?

### External access

GlareDB deployments are protected with randomly generated usernames and
passwords for use with external clients. A cryptographically secure random
number generator is used during generation. Credentials are only valid for a
single GlareDB deployment, and only members of the organization containing the
deployment can generate credentials. Credentials can be revoked at any time.

### Internal access

Production environments are limited to a small number of GlareDB engineers, with
all interactions audited.

Access to customer data is only allowed when debugging customer issues _and_ the
customer has given express consent.

## Reporting vulnerabilities

If you believe you have found a security vulnerability, please contact us at
[security@glaredb.com]. Select members of the team are automatically notified of
all reports sent to this address.

When you send a report for a possible vulnerability, you should expect the
following:

- Acknowledgement of the report within one business day.
- A timeline for mitigating the issue within three business days.
- Updates on resolving the issue.

In some cases, we may request additional information to more accurately assess
the vulnerability. Any information shared will be treated as confidential.

## SOC2 compliance

We are in the process of achieving SOC 2 Type 2 compliance.

[security@glaredb.com]: mailto:security@glaredb.com
