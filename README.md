# Postgres SQL Study
This is my notes for Postgres SQL Study

## MacOS Installation

### 1. Install by Brew
```
brew install postgres
```

### 2. Start the postgres service
```
pg_ctl -D /opt/homebrew/var/postgres start
```

### 3. Login to the default DB
```
psql postgres
```

### 4. List all tables
```
\l
```

### 5. Create a dvdrental database
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
pg_restore -d dvdrental dvdrental.tar 
```

### 9. Login to dvdrental database to verify tables are inplace
Login
```
psql -d dvdrental
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
```
pg_ctl -D /opt/homebrew/var/postgres stop
```

