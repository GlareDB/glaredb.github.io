---
title: Installation
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

1. Install and start the GlareDB binary by running the following in a shell:

    ```shell
    curl https://glaredb.com/install.sh | sh

    ./glaredb
    ```

2. Start writing SQL! You can try out the below to query a Parquet file hosted
    on GitHub over HTTP. This file contains NYC real estate transactions from
    January 2022.

    ```sql
    SELECT *
    FROM read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/nyc_sales/sale_year=2022/sale_month=1/f55363e2587849bcb25c057be706c69d-0.parquet');
    ```

3. Download a file and query it locally. [Here is a file with the next month
    of transaction data.] After downloading it, query it using its relative or
    absolute path.

    ```sql
    -- Relative path to the same directory from which you started the GlareDB CLI
    SELECT * FROM read_parquet('./f55363e2587849bcb25c057be706c69d-0.parquet');

    -- Absolute path to the file
    SELECT * FROM read_parquet('/Users/username/Downloads/f55363e2587849bcb25c057be706c69d-0.parquet');

    ```

4. Query a remote Postgres database using the `read_postgres()`
    function:

        ```sql
        SELECT * FROM read_postgres(
        'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres', --connection
        'public', --schema name
        'customer' --table name
        );
        ````

5. Join between the local Parquet file and the remote Postgres database to
    get a count of number of sales per NYC borough, and include the names of the
    NYC borough where the sales took place:

    ```sql
    SELECT
        COUNT(sales.sale_date),
        lookup.borough_name
    FROM
    read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/nyc_sales/sale_year=2022/sale_month=1/f55363e2587849bcb25c057be706c69d-0.parquet') sales
    JOIN
        read_postgres(
            'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres',
            'public',
            'borough_lookup'
        ) lookup
    ON sales.borough = lookup.borough_id
    GROUP BY lookup.borough_name;
    ```

6. Save your data for easy access later using the previous query and `COPY TO`:

    ```sql
    COPY (
        SELECT
            COUNT(sales.sale_date),
            lookup.borough_name
        FROM
            read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/nyc_sales/sale_year=2022/sale_month=1/f55363e2587849bcb25c057be706c69d-0.parquet') sales
        JOIN
            read_postgres(
                'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres',
                'public',
                'borough_lookup'
            ) lookup
        ON sales.borough = lookup.borough_id
        GROUP BY lookup.borough_name
    ) TO './my_joined_data.parquet';

    SELECT *
    FROM './my_joined_data.parquet';
    ```

7. If you're using [GlareDB Cloud], create new tables that will
    persist in Cloud storage using:

    ```sql
    CREATE TABLE my_new_table AS
    SELECT *
    FROM read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/nyc_sales/sale_year=2022/sale_month=1/f55363e2587849bcb25c057be706c69d-0.parquet');

    SELECT *
    FROM my_new_table;
    ```

## Quickstart with SQL using Python in a Jupyter Notebook

1. Create and activate a new Python environment with:

   ```shell
   python -m venv .venv
   source .venv/bin/activate
   ```

2. Install GlareDB, PyArrow, and Jupyter Notebooks with:

   ```shell
   pip install 'glaredb[pandas]'
   pip install pyarrow
   pip install jupyter
   ```

3. Open your Jupyter notebook

   ```shell
   jupyter notebook
   ```

4. In your notebook, import GlareDB and set up your connection

   ```python
   import glaredb

   con = glaredb.connect()
   ```

5. Start writing SQL! You can try out the below to query a Parquet file hosted
   on GitHub over HTTP. This file contains NYC real estate transactions from
   January 2022.

   ```python
   df = con.sql(
       """
           SELECT *
           FROM read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/nyc_sales/sale_year=2022/sale_month=1/f55363e2587849bcb25c057be706c69d-0.parquet');
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
           FROM read_parquet('./f55363e2587849bcb25c057be706c69d-0.parquet');
       """
   ).to_pandas()


   # Absolute path to the file
   df = con.sql(
       """
           SELECT *
           FROM read_parquet('/Users/username/Downloads/f55363e2587849bcb25c057be706c69d-0.parquet');
       """
   ).to_pandas()

   df
   ```

7. Query a remote Postgres database using the `read_postgres()`
   function:

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
           read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/nyc_sales/sale_year=2022/sale_month=1/f55363e2587849bcb25c057be706c69d-0.parquet') sales
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

9. Save your data for easy access later using the previous query and `COPY TO`:
   TODO: This currently errors. Remove if not quickly resolved.

   ```python
   con.sql(
       """
           COPY (
               SELECT
                   COUNT(sales.sale_date),
                   lookup.borough_name
               FROM
                   read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/nyc_sales/sale_year=2022/sale_month=1/f55363e2587849bcb25c057be706c69d-0.parquet') sales
               JOIN
                   read_postgres(
                       'postgresql://demo:demo@pg.demo.glaredb.com:5432/postgres',
                       'public',
                       'borough_lookup'
                   ) lookup
               ON sales.borough = lookup.borough_id
               GROUP BY lookup.borough_name
           ) TO './my_joined_data.parquet';
       """
   )

   df = con.sql(
       """
           SELECT *
           FROM './my_joined_data.parquet';
       """
   ).to_pandas()

   df
   ```

10. If you're using [GlareDB Cloud], create new tables that will
    persist in Cloud storage using:

    ```python
    con.sql(
        """
            CREATE TABLE my_new_table AS
            SELECT *
            FROM read_parquet('https://github.com/GlareDB/tutorial_data/raw/main/nyc_sales/sale_year=2022/sale_month=1/f55363e2587849bcb25c057be706c69d-0.parquet');
        """
    )

    df = con.sql(
        """
            SELECT *
            FROM my_new_table;
        """
    ).to_pandas()

    df
    ```

[GlareDB Cloud]: https://console.glaredb.com
[Here is a file with the next month of transaction data.]: https://github.com/GlareDB/tutorial_data/raw/main/nyc_sales/sale_year=2022/sale_month=2/f55363e2587849bcb25c057be706c69d-0.parquet
