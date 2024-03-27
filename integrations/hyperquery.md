---
layout: default
title: Hyperquery
parent: Integrations
---

# Using GlareDB in Hyperquery

[Hyperquery] is a data notebook built for speed, visibility, and collaboration.
Hyperquery provides the ability to write and execute SQL queries or Python cells
directly within a rich graphical interface.

## Running GlareDB in Hyperquery

To get started, select an existing notebook, or create a new one.

To install GlareDB in the notebook type `/`, then select **Python block**. This
will place a new block for executing python in the notebook, which will be used
to to install the [glaredb python library].

![python block]

Execute the following command in the code block:

```shell
pip install glaredb
```

Next, in a new **Python block**, import and use glaredb:

```python
import glaredb

con = glaredb.connect()
con.sql("SELECT 'hello from hyperquery';").to_pandas()
```

{: .important }

> [Pandas] is in scope. GlareDB provides interop with both [Pandas] and [Polars]
> dataframe libraries. For more information, refer to [GlareDB Python documentation].

Executing `SELECT 'hello from hyperquery';` will produce output like:

![success]

## Connecting to GlareDB Cloud from Hyperquery

Sign in or sign up with [GlareDB Cloud]. Upon signing up, a free deployment is
instantly created and ready to be used. Obtain the Python connection details for
a deployment by clicking the **Connect** button and selecting the **Python** tab.

![connect button]

![connect python]

In a **Python block**, use the connection URI when calling `glaredb.connect`:

```python
import glaredb

cloud_uri = "glaredb://user:password@org.remote.glaredb.com:6443/db_name"

con = glaredb.connect(cloud_uri)
```

Hyperquery has access to all of the resources in the GlareDB Cloud deployment
through [Hybrid Execution]. Data in the notebook, including [Pandas] and [Polars]
dataframes can be joined with data in GlareDB Cloud.

[Hyperquery]: https://www.hyperquery.ai/
[glaredb python library]: https://pypi.org/project/glaredb/
[python block]: /assets/images/glaredb/hyperquery/python-block.png
[Pandas]: https://github.com/pandas-dev/pandas
[Polars]: https://github.com/pola-rs/polars
[GlareDB Python documentation]: /glaredb/python
[success]: /assets/images/glaredb/hyperquery/success.png
[GlareDB Cloud]: https://console.glaredb.com
[connect button]: /assets/images/glaredb/hyperquery/connect-button.png
[connect python]: /assets/images/glaredb/hyperquery/connect_python.png
[Hybrid Execution]: /glaredb/hybrid-execution/
