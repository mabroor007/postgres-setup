# postgres-setup-docker

Setup

### Step 1
Pull latest postgres alpine image from docker hub.

### Step 2
use following command to run Postgres Container


`docker run -d --name my-db-server -p 5432:5432 -e POSTGRES_PASSWORD=pwd postgres:alpine`

### Step 3
Open container shell by following command


`docker exec -it my-db-server bash`

### Step 4
Open psql shell by this command


`psql -U postgres`

### Step 5
Create a Database


```SQL
CREATE DATABASE test;
```

### Step 6
Connect to a Database


 In psql shell type


    `\c name_of_database`


**Or**


 From Container Shell type
 
 
    `psql -h localhost -p 5432 -d name_of_database -U postgres`



### Step 7
Deleting a database


```SQL
DROP DATABASE name_of_database;
```


CareFull its Dangerous.



### Step 8
Exiting psql shell


`\q`




## Usage 

CHEAT SHEAT
| Command | Functionality |
|---|------|
| \l | List of all the databases |
| \d | List of all the Tables in Current database |
| \d table_name | Details of table |
| \dt | Just the list of tables |

---
# SQL 
Create a Table 
```SQL
CREATE TABLE person ( id INT,
                       name VARCHAR(50),
                       date_of_birth VARCHAR(50),
                       gender VARCHAR(7));
```


Delete a Table
```SQL
DROP TABLE table_name;
```


Create a table with constraints


```SQL 
CREATE TABLE person ( id BIGSERIAL NOT NULL PRIMARY KEY,  
                       first_name VARCHAR(50) NOT NULL,  
                       last_name VARCHAR(50) NOT NULL,  
                       gender VARCHAR(7) NOT NULL,  
                       date_of_birth DATE NOT NULL,  
                       email VARCHAR(150) );
```


Inserting entry into table
```SQL
INSERT INTO person ( first_name, last_name, gender, date_of_birth )
            VALUES ( 'Jhon', 'Doe', 'MALE', DATE '1998-12-12' );
```
   **OR**


```SQL
INSERT INTO person ( first_name, last_name, gender, date_of_birth, email )
            VALUES ( 'Martin', 'Guptil', 'MALE', DATE '1890-8-30', 'guptil@gmail.com' );
```


