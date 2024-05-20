---
title: Connect to GlareDB in Go
layout: default
nav_order: 3
parent: Tutorials
---

# Connect to GlareDB in Go

GlareDB is Postgres-compatible, allowing connections to GlareDB in Go to be
made using [`lib/pq`](https://github.com/lib/pq).

Connections can be established with either [GlareDB Cloud] or a self-hosted or
locally running instance of GlareDB.

## Connecting to [GlareDB Cloud]

If you haven't already, sign up for [GlareDB Cloud]. There is a free tier
to get started. For more information, refer to the
[GlareDB Cloud documentation].

Connection details for a deployment can be accessed from the SQL workspace by
clicking the **Connect** button, then selecting the **Postgres** tab and **Go**
sub-tab.

![connect]

The tab contains a thorough example of connecting to and querying your GlareDB
Cloud deployment.

Notice that we treat it like any other Postgres database:

```go
db, err := sql.Open("postgres", "<connection_string>")
```

## Connecting to a local server for testing

To connect to a local server for testing purposes, you need to construct a
Postgres connection string with the appropriate details.

By default, GlareDB runs on port 6543. To install GlareDB, refer to the
[installation instructions]. For more details on running GlareDB in server mode,
refer to the help output:

```shell
glaredb server --help
```

Assuming a locally running GlareDB server on port 6543, a connection can be made
as follows:

```go
package main

import (
    "database/sql"
    "log"
    "os"

    _ "github.com/lib/pq"
)

func main() {
    conn := "host=localhost port=6543 dbname=glaredb sslmode=disable"

    db, err := sql.Open("postgres", conn)
    if err != nil {
        log.Fatal(err)
    }

    var s sql.NullString
    row := db.QueryRow("SELECT 'Connected to GlareDB!'")
    if err := row.Scan(&s); err != nil {
        log.Fatal(err)
    }

    log.Println(s.String)
    os.Exit(0)
}
```

[GlareDB Cloud]: https://console.glaredb.com
[GlareDB Cloud documentation]: /cloud/
[connect]: /assets/images/tutorials/connect-go.png
[installation instructions]: /introduction/locally-cli.html#install
