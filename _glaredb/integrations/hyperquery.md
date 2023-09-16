---
layout: default
title: Hyperquery
parent: Integrations
---

# Hyperquery

[Hyperquery] is a data notebook built for speed, visibility, and collaboration.
You can write and execute SQL queries or Python cells directly within a WYSIWYG
(what you see is what you get) notebook, and augment this work with rich
formatting options.

In this guide, we'll walk through how to get starting with GlareDB in
Hyperquery.

## Running GlareDB in Hyperquery

To get started, first either select an existing notebook, or create a new.
To create a new notebook, click **Create a new page**.

![create]

And now we have a new notebook ready to go. To install GlareDB in the notebook
type `/`, then select **Python block**.

![python block]

This will place a new block for executing python in the notebook. We'll use this
first block to install the [glaredb python library]. To do so, execute the
following command in the code block:

```text
!pip install glaredb
```

If everything installed succesffuly, you should be able to import and use
glaredb in a new Python block:

```python
import glaredb

con = glaredb.connect()
con.sql("select 'hello from hyperquery").to_pandas()
```

And you should see the follwing in your notebook:

![success]

## Connecting to GlareDB Cloud from Hyperquery

Connecting to [GlareDB Cloud] to your deployment is easy. If you're a new user,
a deployment is automatically created for you. If you have multiple, select the
one that you'd like to connect with. To get connection details for the
deployment, click the **Connect** button then select the **Python** tab. This
will provide a connection URI that you can use when connecting via the python
library.

![connect]

Paste the URI from the prior step in the connect function:

```python
import glaredb

con = glaredb.connect("glaredb://user:password@org.remote.glaredb.com:6443/deployment")
```

And once connected you can now query all tables in your GlareDB Cloud deployment
from Hyperquery.

![cloud]

When connecting to GlareDB Cloud through the python library, [Hybrid Execution]
will automatically be enabled. This lets you join data from your GlareDB Cloud
deployment with data that exists in your Hyperquery notebook, like Pandas data
frames.

[Hyperquery]: https://www.hyperquery.ai/
[GlareDB Cloud]: https://console.glaredb.com
[create]: /assets/images/hyperquery/create.png
[cloud]: /assets/images/hyperquery/cloud.png
[Hybrid Execution]: /glaredb/hybrid-execution/
[connect]: /assets/images/hyperquery/connect.png
[success]: /assets/images/hyperquery/success.png
[python block]: /assets/images/hyperquery/python-block.png
[glaredb python library]: https://pypi.org/project/glaredb/
