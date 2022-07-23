# Postgres SQL Study
This is my notes for Postgres SQL Study

## MacOS Installation

1. Install by Brew
```
brew install postgres
```

2. Start the postgres service
```
pg_ctl -D /opt/homebrew/var/postgres start
```

2. Login to the default DB
```
psql postgres
```

3. List all tables
```
\l
```

4. Create a dvdrental database
```
create database dvdrental
```

5. Import dvdrental data to dvdrental database
Exit psql and execute the following commmand
```
pg_restore -d dvdrental dvdrental.tar 
```

6. Login to dvdrental database to verify tables are inplace
Login
```
psql -D dvdrental
```

Describe all tables
```
\dt
```

