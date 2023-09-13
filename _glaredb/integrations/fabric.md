---
layout: default
title: Fabric
parent: Integrations
---

# Fabric

[Microsoft Fabric] provides a suite of data analytics, data engineering, and BI
tools on the Azure platform.

In this guide, we'll walk through how to install and run GlareDB using a
Notebook in Fabric.

## Running GlareDB in a notebook

The first step to running GlareDB in Fabric is to create a notebook. A notebook
can be created by selecting **Notebook (Preview)** from the **Create** tab.

![create]

Once created, you'll be dropped into the notebook where you can begin executing
python cells.

Now we're able to install the [glaredb python library] by executing the
following in a python cell:

```text
!pip install glaredb
```

If everything installed successfully, you should be able to import and use
glaredb:

```python
import glaredb

con = glaredb.connect()
con.sql("select 'hello from fabric'").show()
```

And this is what the output should look like:

![success]

## Connecting to GlareDB Cloud from Fabric

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
from Fabric.

![cloud]

When connecting to GlareDB Cloud through the python library, [Hybrid Execution]
will automatically be enabled.

[Microsoft Fabric]: https://www.microsoft.com/en-us/microsoft-fabric
[glaredb python library]: https://pypi.org/project/glaredb/
[GlareDB Cloud]: https://console.glaredb.com
[Hybrid Execution]: /glaredb/hybrid-execution/
[create]: /assets/images/fabric/create.png
[cloud]: /assets/images/fabric/cloud.png
[success]: /assets/images/fabric/success.png
[connect]: /assets/images/fabric/connect.png
