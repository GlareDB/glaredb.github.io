---
layout: default
title: Securing connections with SSH tunnels
parent: "Step 1: Connect your data sources"
---

# Securing connections with SSH tunnels

{: .important}

> Currently only MySQL and Postgres data sources support SSH tunnels

For scenarios whereby a data source does not have a public access point, GlareDB
can use a tunnel to make the connection. SSH tunnels are specified per
deployment, and can be reused by multiple data sources for that deployment.

## Creating and using SSH tunnels using SQL

1. Create the tunnel

   ```sql
   CREATE TUNNEL example_tunnel FROM ssh OPTIONS (
      host = '1.2.3.4',
      port = '22',
      user = 'example_ssh_user'
   );
   ```

2. Get the public key and add it to your SSH server

   ```sql
   SELECT public_key FROM glare_catalog.ssh_keys
      WHERE ssh_tunnel_name = 'example_tunnel';
   ```

3. Create the data source with the tunnel

   ```sql
   CREATE EXTERNAL DATABASE my_pg
      FROM postgres
      TUNNEL example_tunnel
      OPTIONS ( connection_string = '<connection-string>' );
   ```

## Creating and using SSH tunnels using GlareDB Cloud

You can create SSH tunnels from the **SQL workspace**:

1. From the **SQL workspace** select the **SSH tunnels** panel from the sidebar

   ![SSH tunnel settings]

2. Click the **+** button at the top right, or **Create tunnel**. Add the host,
   port and user for the SSH server.

   ![Create SSH tunnel]

3. After creating the tunnel a public key will be presented. Add this key to
   your SSH server (for example `~/.ssh/authorized_keys`)

   ![SSH tunnel public key]

[SSH tunnel settings]: /assets/images/data-sources/ssh_tunnels_sidebar.png
[Create SSH tunnel]: /assets/images/data-sources/create_ssh_tunnel.png
[SSH tunnel public key]: /assets/images/data-sources/public-key.png
