# Docker
This is my notes for Postgres SQL Study for Docker

## Docker walkthrough

### 1. Go to https://hub.docker.com and search for ***postgres***
![docker hub](/img/docker01.png)

### 2. Select the official image. This is the image mantained by the Docker PostgresSQL Community
![docker hub2](/img/docker02.png)
or click the following link to go directly to this page
https://hub.docker.com/_/postgres

### 3. Start the Postgres Container
```
docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres
```
- ```--name some-postgres``` set the container name
- ```-e POSTGRES_PASSWORD=mysecretpassword``` set the password of the default user ```postgres```
- ```-d postgres``` create a initial DB named ```postgres```

### 4. List all running container to ensure the postgres is running
```
docker ps
```

Sample output:
```
❯ docker ps
CONTAINER ID   IMAGE      COMMAND                  CREATED          STATUS          PORTS      NAMES
a3b14a12580a   postgres   "docker-entrypoint.s…"   33 minutes ago   Up 33 minutes   5432/tcp   some-postgres
```


### 5. Execute the internal ***psql*** client to the container
```
docker exec -it some-postgres psql -U postgres
```

### 6. List all tables
```
\l
```

### 7. Create a dvdrental database
```
create database dvdrental
```

### 6. Exit psql 
```
\q
```

### 7. Download and unzip the dvdrental data
```
curl -O https://www.postgresqltutorial.com/wp-content/uploads/2019/05/dvdrental.zip && unzip dvdrental.zip
```

### 8. Execute the following commmand to import the data
```
docker exec -i some-postgres pg_restore -U postgres -v -d dvdrental < dvdrental.tar
```

### 9. Login to dvdrental database to verify tables are inplace
Login
```
docker exec -it some-postgres psql -U postgres -d dvdrental
```

### 10. Describe all tables
```
\dt
```

### 11. List the first 10 actor from the actor table
```
select * from actor limit 10;
```

### 12. sample output
```
❯ psql -d dvdrental
psql (14.4)
Type "help" for help.

dvdrental=# \dt
               List of relations
 Schema |     Name      | Type  |    Owner
--------+---------------+-------+--------------
 public | actor         | table | kaptenjeffry
 public | address       | table | kaptenjeffry
 public | category      | table | kaptenjeffry
 public | city          | table | kaptenjeffry
 public | country       | table | kaptenjeffry
 public | customer      | table | kaptenjeffry
 public | film          | table | kaptenjeffry
 public | film_actor    | table | kaptenjeffry
 public | film_category | table | kaptenjeffry
 public | inventory     | table | kaptenjeffry
 public | language      | table | kaptenjeffry
 public | payment       | table | kaptenjeffry
 public | rental        | table | kaptenjeffry
 public | staff         | table | kaptenjeffry
 public | store         | table | kaptenjeffry
(15 rows)

dvdrental=# select * from actor limit 10;
 actor_id | first_name |  last_name   |      last_update
----------+------------+--------------+------------------------
        1 | Penelope   | Guiness      | 2013-05-26 14:47:57.62
        2 | Nick       | Wahlberg     | 2013-05-26 14:47:57.62
        3 | Ed         | Chase        | 2013-05-26 14:47:57.62
        4 | Jennifer   | Davis        | 2013-05-26 14:47:57.62
        5 | Johnny     | Lollobrigida | 2013-05-26 14:47:57.62
        6 | Bette      | Nicholson    | 2013-05-26 14:47:57.62
        7 | Grace      | Mostel       | 2013-05-26 14:47:57.62
        8 | Matthew    | Johansson    | 2013-05-26 14:47:57.62
        9 | Joe        | Swank        | 2013-05-26 14:47:57.62
       10 | Christian  | Gable        | 2013-05-26 14:47:57.62
(10 rows)

```

### 13. Stop PostgreSQL service
Exit from the psql
```
\q
```

Stop the container
```
docker stop some-postgres
```

## Docker with persistance storage

### 1. Create volume
```
docker volume create pg-data
```

### 2. Inspect volumes 
```
docker volume ls
```

### 3. Run the Container with the create volume
```
docker run -d \                                                                                                                                           
        --name pg-with-vol \
        -e POSTGRES_PASSWORD=mysecretpassword \
        -v pg-data:/var/lib/postgresql/data \
        postgres
```

## Docker Compose 
Instead of the CLI way, we could put the application configuration in a yaml file know as Docker Compose. It's a yaml config file that is understand by docker to start and stop of a Docker container

Create the following docker-compose.yaml file
```
version: '3.1'

services:

  db:
    image: postgres
    restart: always
    environment:
      POSTGRES_PASSWORD: mysecretpassword

```

### 2. To start Postgres just run the following command in the same location of the yaml file
```
docker-compose up
```
