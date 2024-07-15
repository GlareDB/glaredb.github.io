---
layout: default
title: INSERT INTO
parent: SQL commands
grand_parent: Reference
---

# INSERT INTO

Insert data into a native table.

{: .important}

> GlareDB does not yet support UPDATE for native tables.

## Syntax

```sql
INSERT INTO table_name VALUES (value)[, ... ];
```

| Field        | Description                           |
| ------------ | ------------------------------------- |
| `table_name` | Name of the table.                    |
| `value`      | A value set to insert into the table. |

## Examples

In this example we'll first [`CREATE`] a simple users table, then insert two
users into it.

```sql
CREATE TABLE public.users ( name text, email text );

INSERT INTO public.users AS VALUES
  ('Pris', 'pris@stratton.net'),
  ('Eldon Tyrell', 'ceo@tyrell.corp');
```

### INSERT INTO Delta Tables

You can insert into Delta tables that you have added as [external tables] in
GlareDB. Be sure to enable write permissions for this external table in
GlareDB. When doing this, you will write data to the actual Delta table outside
of GlareDB

```sql
CREATE EXTERNAL TABLE my_delta
FROM delta
OPTIONS (location './my_delta');

ALTER TABLE my_delta SET ACCESS_MODE TO READ_WRITE;

INSERT INTO my_delta
  SELECT * FROM
    my_postgres.public.my_table a
  WHERE
    a.id > 1000
```

Check out the video below for a more hands-on example:
<!-- markdownlint-disable -->
<iframe width="560" height="315" src="https://www.youtube.com/embed/7W9Y_zZEENg?si=vNupX8HS8AnOrm_O" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>
<!-- markdownlint-enable -->

[`CREATE`]: /reference/sql-commands/create-table/
[external tables]: /reference/sql-commands/create-external-table/
