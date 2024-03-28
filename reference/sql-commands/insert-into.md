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

[`CREATE`]: /glaredb/sql-commands/create-table/
