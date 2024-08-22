---
title: Quickstart
layout: default
nav_order: 1
parent: Getting Started
---

<details open markdown="block">
  <summary>
    Table of contents
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Quickstart with SQL using the GlareDB CLI

1. Install and start the GlareDB binary by running the following in a shell.
When starting GlareDB, use `-f` and specify a path so that GlareDB will 
create a directory to persist your tables after you close the session.
You can also leave this blank for an in-memory-only session.


   ```shell
   > curl https://glaredb.com/install.sh | sh
   > ./glaredb -f ./my_db_path
   ```

2. Start writing SQL! You can try out the below to query a Parquet file hosted
   on GitHub over HTTP. This file contains NYC real estate transactions from
   January 2022.

   ```sql
   SELECT *
   FROM read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/quickstart_data/nyc_sales-2022_01.parquet');
   ```

3. Download a file and query it locally. [Here is a file with the next month
   of transaction data.] After downloading it, query it using its relative or
   absolute path.

   ```sql
   -- Relative path to the same directory from which you started the GlareDB CLI
   SELECT * FROM read_parquet('./nyc_sales-2022_02.parquet');

   -- Absolute path to the file
   SELECT * FROM read_parquet('/Users/username/Downloads/nyc_sales-2022_02.parquet');

   ```

4. Query a remote Postgres database using the `read_postgres()` function:

   ```sql
   SELECT * FROM read_postgres(
   'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres', --connection
   'public', --schema name
   'customer' --table name
   );
   ```

5. Join between the local Parquet file and the remote Postgres database to
   get a count of number of sales per NYC borough, and include the names of the
   NYC borough where the sales took place:

   ```sql
   SELECT
       COUNT(sales.sale_date),
       lookup.borough_name
   FROM
        read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/quickstart_data/nyc_sales-2022_01.parquet') sales
   JOIN
       read_postgres(
           'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres',
           'public',
           'borough_lookup'
       ) lookup
   ON sales.borough = lookup.borough_id
   GROUP BY lookup.borough_name;
   ```

6. Save your data for easy access later by creating a table with the previous query:

   ```sql
   CREATE TABLE sales_aggregate_by_borough AS
       SELECT
           COUNT(sales.sale_date),
           lookup.borough_name
       FROM
           read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/quickstart_data/nyc_sales-2022_01.parquet') sales
       JOIN
           read_postgres(
               'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres',
               'public',
               'borough_lookup'
           ) lookup
       ON sales.borough = lookup.borough_id
       GROUP BY lookup.borough_name;

   SELECT *
   FROM sales_aggregate_by_borough;
   ```

7. Or export your data to a Parquet (or other) file for easy access later by wrapping your query in a `COPY TO` statement:

   ```sql
   COPY (
       SELECT
           COUNT(sales.sale_date),
           lookup.borough_name
       FROM
           read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/quickstart_data/nyc_sales-2022_01.parquet') sales
       JOIN
           read_postgres(
               'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres',
               'public',
               'borough_lookup'
           ) lookup
       ON sales.borough = lookup.borough_id
       GROUP BY lookup.borough_name
   ) TO './sales_aggregate_by_borough.parquet';

   SELECT *
   FROM './sales_aggregate_by_borough.parquet';
   ```


## Quickstart with SQL using Python in a Jupyter Notebook

1. Create and activate a new Python environment with:

   ```shell
   > python -m venv .venv
   > source .venv/bin/activate
   ```

2. Install GlareDB, PyArrow, and Jupyter Notebooks with:

   ```shell
   > pip install 'glaredb[pandas]' pyarrow jupyter
   ```

3. Open your Jupyter notebook

   ```shell
   > jupyter notebook
   ```

4. In your notebook, import GlareDB and set up your connection. 
When instantiating your connection specify a path so that GlareDB will 
create a directory to persist your tables after you close the session.
(You can also leave this blank for an in-memory-only session.)

   ```python
   import glaredb

   con = glaredb.connect('./my_db_path')
   ```

5. Start writing SQL! You can try out the below to query a Parquet file hosted
   on GitHub over HTTP. This file contains NYC real estate transactions from
   January 2022.

   ```python
   df = con.sql(
       """
           SELECT *
           FROM read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/quickstart_data/nyc_sales-2022_01.parquet');
       """
   ).to_pandas()

   df
   ```

6. Download a file and query it locally. [Here is a file with the next month
   of transaction data.] After downloading it, query it using its relative or
   absolute path.

   ```python
   # Relative path to the same directory from which you started the GlareDB CLI
   df = con.sql(
       """
           SELECT *
           FROM read_parquet('./nyc_sales-2022_02.parquet');
       """
   ).to_pandas()


   # Absolute path to the file
   df = con.sql(
       """
           SELECT *
           FROM read_parquet('/Users/username/Downloads/nyc_sales-2022_02.parquet');
       """
   ).to_pandas()

   df
   ```

7. Query a remote Postgres database using the `read_postgres()` function:

   ```python
   df = con.sql(
       """
           SELECT * FROM read_postgres(
               'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres', --connection
               'public', --schema name
               'customer' --table name
           );
       """
   ).to_pandas()

   df
   ```

8. Join between the local Parquet file and the remote Postgres database to
   get a count of number of sales per NYC borough, and include the names of the
   NYC borough where the sales took place:

   ```python
   df = con.sql(
       """
           SELECT
               COUNT(sales.sale_date),
               lookup.borough_name
           FROM
           read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/quickstart_data/nyc_sales-2022_01.parquet') sales
           JOIN
               read_postgres(
                   'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres',
                   'public',
                   'borough_lookup'
               ) lookup
           ON sales.borough = lookup.borough_id
           GROUP BY lookup.borough_name;
                   );
       """
   ).to_pandas()

   df
   ```

9. Save your data for easy access later by creating a table with the previous query:

   ```python
   con.sql(
       """
           CREATE TABLE sales_aggregate_by_borough AS
               SELECT
                   COUNT(sales.sale_date),
                   lookup.borough_name
               FROM
                   read_parquet(https://github.com/GlareDB/tutorial_data/raw/main/quickstart_data/nyc_sales-2022_01.parquet) sales
               JOIN
                   read_postgres(
                       'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres',
                       'public',
                       'borough_lookup'
                   ) lookup
               ON sales.borough = lookup.borough_id
               GROUP BY lookup.borough_name;
       """
   )

   df = con.sql(
       """
           SELECT *
           FROM sales_aggregate_by_borough;
       """
   ).to_pandas()

   df
   ```

10. Or export your data to a Parquet (or other) file for easy access later by wrapping your query in a `COPY TO` statement::

   ```python
   con.sql(
       """
           COPY (
               SELECT
                   COUNT(sales.sale_date),
                   lookup.borough_name
               FROM
                   read_parquet(https://github.com/GlareDB/tutorial_data/raw/main/quickstart_data/nyc_sales-2022_01.parquet) sales
               JOIN
                   read_postgres(
                       'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres',
                       'public',
                       'borough_lookup'
                   ) lookup
               ON sales.borough = lookup.borough_id
               GROUP BY lookup.borough_name
           ) TO './sales_aggregate_by_borough.parquet';
       """
   )

   df = con.sql(
       """
           SELECT *
           FROM './sales_aggregate_by_borough.parquet';
       """
   ).to_pandas()

   df
   ```

## Next Steps

That's it! Up next you can:

- [Read more about GlareDB Cloud] or [sign up]
- Check out the [different data sources GlareDB supports]
- Check out the [GlareDB YouTube channel] for more step-by-step examples
- [Star us on GitHub]
- [Open a GitHub Issue] for bug reports or feature requests
- [Join our Discord] if you have any questions or want to chat

[Here is a file with the next month of transaction data.]: https://github.com/GlareDB/tutorial_data/raw/main/quickstart_data/nyc_sales-2022_02.parquet
[Read more about GlareDB Cloud]: ../cloud/index
[sign up]: https://console.glaredb.com
[different data sources GlareDB supports]: ../data-sources/index
[GlareDB YouTube channel]: https://www.youtube.com/channel/UC0BAh5qyH65kecM9XfLqfkQ
[Star us on GitHub]: https://github.com/GlareDB/glaredb
[Open a GitHub Issue]: https://github.com/GlareDB/glaredb/issues/new/choose
[Join our Discord]: https://discord.gg/cZ7A6Bj3MW
