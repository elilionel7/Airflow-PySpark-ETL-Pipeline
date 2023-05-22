# Apache Airflow & PySpark ETL Pipeline README

This README provides information about two Python scripts, `dags.py` and `transformation.py`, which together perform an Extract, Transform, Load (ETL) pipeline using Apache Airflow for task scheduling and PySpark for data processing..

## Requirements

- Python 3.6 or later
- PySpark 3.0.0 or later
- Apache Airflow
- PostgreSQL JDBC driver (Download: https://jdbc.postgresql.org/download.html)

# Usage

1. Ensure the transformation.py module is in your Python path or in the same directory as dags.py. This module should contain the necessary data extraction, transformation, and loading functions.
2. Start your PySpark session by executing the transformation.py script. Ensure that the path to the JDBC driver jar file (postgresql-42.5.2.jar) is correct in the Spark session configuration.
3. The transformation.py script connects to a PostgreSQL database on localhost, port 5432, with database name 'postgres'. Make sure to replace 'username' and 'mypassword' with your own PostgreSQL username and password.
4. Run Apache Airflow and schedule the dags.py script. This script will use Apache Airflow to manage the scheduling and execution of the ETL pipeline.

## Description of Files

The `dags.py` and `transformation.py` files together form an ETL pipeline that uses PySpark for data processing and Apache Airflow for task scheduling and management.

### dags.py

This file defines an Airflow DAG (Directed Acyclic Graph) which represents a collection of all the tasks you want to run, organized in a way that reflects their relationships and dependencies. The ETL pipeline is encapsulated within a single Python function (`etl()`), which is scheduled to run daily.

The `etl()` function performs the following tasks:
1. Extracts movies data from a PostgreSQL database into a Spark dataframe.
2. Extracts users data from the same database into another Spark dataframe.
3. Transforms the extracted data by calculating the average ratings for each movie.
4. Loads the transformed data back into the PostgreSQL database.

### transformation.py

This file contains the functions necessary for data extraction, transformation, and loading. Each function corresponds to a specific step in the ETL pipeline.

The `extract_movies_to_df()` and `extract_users_to_df()` functions read data from the 'movies' and 'users' tables in a PostgreSQL database, respectively, and return them as PySpark dataframes.

The `transform_avg_ratings(movies_df, users_df)` function takes these two dataframes, calculates the average rating for each movie, and returns a transformed dataframe.

The `load_df_to_db(df)` function takes this transformed dataframe and writes it back to a table named 'avg_ratings' in the PostgreSQL database.

