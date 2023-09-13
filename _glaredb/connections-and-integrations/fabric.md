---
layout: default
title: Fabric
parent: Connections and integrations
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

Once created, you'll be dropped into the notebook where you can begin execution
python cells.

Now we're able to install the [glaredb python library] by execution the
following in a python cell:

```text
!pip install glaredb
```

If everything install successfully, you should now be able to import and run
glaredb:

```python
import glaredb

con = glaredb.connect()
con.sql("select 'hello from fabric'").show()
```

And this is what the output should look like:

![success]

## Connecting to GlareDB Cloud from Fabric

Connecting to GlareDB Cloud from Fabric is easy once you've created a deployment
on GlareDB Cloud. To get connection details for the deployment, click the
**Connect** button then select the **Python** tab. This will provide credentials
that you can use when connecting via the python library.

![connect]

Now that you have your credentials, you can now to GlareDB cloud from Fabric by
providing the credentials to the `connect` function:

```python
import glaredb

con = glaredb.connect("glaredb://user:password@glaredb-better.remote.glaredb.com:6443/deployment")
```

And once connected you can now query all tables in your GlareDB Cloud deployment
from Fabric.

![cloud]

When connecting to GlareDB Cloud through the python library, [Hybrid Execution]
will automatically be enabled.

[Microsoft Fabric]: https://www.microsoft.com/en-us/microsoft-fabric
[glaredb python library]: https://pypi.org/project/glaredb/
[Hybrid Execution]: /glaredb/hybrid-execution/
[create]: /assets/images/fabric/create.png
[cloud]: /assets/images/fabric/cloud.png
[success]: /assets/images/fabric/success.png
[connect]: /assets/images/fabric/connect.png
