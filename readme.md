## pgvector
#  
  >docker run --name pgvector -e POSTGRES_PASSWORD=pg -v pgvect:/var/lib/postgresql/data -e POSTGRES_DB=data -p 5432:5432 -d pgvector/pgvector:pg17
#

# * docker run: This command is used to create and start a new container based on a specified image.
# * --name pgvector: This option assigns the name "pgvector" to the container, making it easier to reference later.
# * -e POSTGRES_PASSWORD=pg: This sets an environment variable that defines the password for the default PostgreSQL user (postgres). In this case, the password is set to "pg".
# * -v pgvect:/var/lib/postgresql/data: This option mounts a Docker volume named "pgvect" to the specified directory inside the container. This ensures that the database data is stored persistently, even if the container is stopped or removed.
# * -e POSTGRES_DB=data: This sets another environment variable that specifies the name of a default database to be created when the PostgreSQL server starts. Here, it’s named "data".
# * -p 5432:5432: This maps port 5432 on your local machine (host) to port 5432 in the container. This allows you to access PostgreSQL running inside the container from your host machine using this port.
# * -d: This flag tells Docker to run the container in detached mode, meaning it will run in the background.
# * pgvector/pgvector:pg17: This specifies the Docker image to use for creating the container. In this case, it’s using the pgvector image compatible with PostgreSQL version 17.

##login into container
#
  docker exec -it pgvector bash

  psql -U postgres -p 5432 -d data
#
## After enter into database we can add pgvector extention
#
  CREATE EXTENSION vector;
#
# * The command CREATE EXTENSION  vector; is used in PostgreSQL to load the pgvector extension into the current database. This extension provides functionality for handling vector data, which is essential for applications involving machine learning and artificial intelligence, particularly for tasks like similarity search and embedding storage.

## Create Database in database
#
 create database ram;
#
## list all the data bases
 # 
  >\l
#
## switch to another database
 #
    >\c ram;
#

## create table and insert data into it
##
    CREATE TABLE embeddings (
    id SERIAL PRIMARY KEY,
    vector VECTOR(3)  -- Specify the dimensionality of your vectors here
   );


  INSERT INTO embeddings (vector) 
  VALUES 
    ('[0.1, 0.2, 0.3]'), 
    ('[0.4, 0.5, 0.6]'), 
    ('[0.7, 0.8, 0.9]');

#

## To see the table 
#
  SELECT * FROM embeddings;
#
 ram=# select * from emb;
 id |    vector
----+---------------
  1 | [0.1,0.2,0.3]
  2 | [0.4,0.5,0.6]
  3 | [0.7,0.8,0.9]


## create a pgvector conatainer with user
## docker run --name pgvector \
-e POSTGRES_USER=postgres \
-e POSTGRES_PASSWORD=pg \
-e POSTGRES_DB=data \
-v pgvect:/var/lib/postgresql/data \
-p 5432:5432 \
-d pgvector/pgvector:pg16


## Create user in pgvector database
# 
  CREATE USER new_username WITH PASSWORD 'your_password';

#
## grant permissions to users
# 
  GRANT ALL PRIVILEGES ON DATABASE data TO new_username;
#




