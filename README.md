# PySpark-ELT-Pipeline
This Python pipeline uses PySpark to extract movie and user data from a PostgreSQL database, performs transformation on the data to calculate average movie ratings, and then loads the transformed data back into the database.

# Requirements
Python 3.6 or later
PySpark 3.0.0 or later
PostgreSQL JDBC driver (Download: https://jdbc.postgresql.org/download.html)
# Usage
Start your PySpark session by executing the script. Ensure that the path to the JDBC driver jar file (postgresql-42.5.2.jar) is correct in the Spark session configuration.
The script connects to a PostgreSQL database on localhost, port 5432, with database name 'postgres', user 'username', and password 'mypassword'.
The script reads the 'movies' and 'users' tables from the PostgreSQL database into Spark dataframes.
The script then calculates the average rating for each movie by grouping on the 'movie_id' field in the users dataframe.
The average rating is then joined to the movies dataframe on the 'movie_id' field.
Finally, the transformed dataframe is written back into the PostgreSQL database, to a table named 'avg_ratings'. This operation overwrites the table if it already exists.
# Functions
The script consists of several functions:

extract_movies_to_df(): Reads the 'movies' table from the PostgreSQL database and returns it as a Spark dataframe.
extract_users_to_df(): Reads the 'users' table from the PostgreSQL database and returns it as a Spark dataframe.
transform_avg_ratings(movies_df, users_df): Takes the movies and users dataframes as arguments, calculates the average rating for each movie, and returns a dataframe of movies with the average ratings.
load_df_to_db(df): Takes a dataframe as argument, and writes it to the 'avg_ratings' table in the PostgreSQL database. Overwrites the table if it already exists.




