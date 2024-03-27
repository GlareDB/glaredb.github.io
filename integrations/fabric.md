---
layout: default
title: Fabric
parent: Integrations
---

# Fabric

[Microsoft Fabric] provides a suite of data analytics, data engineering, and BI
tools on the Azure platform.

In this guide, we'll walk through how to install and run GlareDB using a
notebook in Fabric.

## Running GlareDB in a Notebook

The first step to running GlareDB in Fabric is to create a notebook. A notebook
can be created by selecting **Notebook (Preview)** from the **Create** tab.

![create]

Once created, you'll be dropped into the notebook where you can begin executing
Python cells.

Now we're able to install the [GlareDB Python library] by executing the
following in a Python cell:

```text
!pip install glaredb
```

If everything installed successfully, you should be able to import and use
GlareDB:

```python
import glaredb

con = glaredb.connect()
con.sql("select 'hello from fabric'").show()
```

And this is what the output should look like:

![success]

## Connecting to GlareDB Cloud from Fabric

[GlareDB Cloud] features fully-managed instances of GlareDB, enabling you
to access your data in notebooks, dashboards and applications. 
[You can sign up here.] If you're a new user, a deployment is automatically
created for you. To get connection details for the deployment, click the 
**Connect** button then select the **Python** tab. This will provide a
connection URI that you can use when connecting via the Python library.

![connect]

Paste the URI from the prior step in the connect function:

```python
import glaredb

con = glaredb.connect("glaredb://user:password@org.remote.glaredb.com:6443/deployment")
```

And once connected you can now query all tables in your GlareDB Cloud deployment
from Fabric.

![cloud]

When connecting to GlareDB Cloud through the Python library, [Hybrid Execution]
will automatically be enabled.

[Microsoft Fabric]: https://www.microsoft.com/en-us/microsoft-fabric
[GlareDB Python library]: https://pypi.org/project/glaredb/
[GlareDB Cloud]: https://console.glaredb.com
[Hybrid Execution]: /glaredb/hybrid-execution/
[create]: /assets/images/glaredb/fabric/create.png
[cloud]: /assets/images/glaredb/fabric/cloud.png
[success]: /assets/images/glaredb/fabric/success.png
[connect]: /assets/images/glaredb/fabric/connect_python.png
[You can sign up here.]: https://console.glaredb.com/
