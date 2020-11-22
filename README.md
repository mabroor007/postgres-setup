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
                       email VARCHAR(150) NOT NULL UNIQUE );
```


Inserting entry into table
```SQL
INSERT INTO person ( first_name, last_name, gender, date_of_birth, email )
            VALUES ( 'Jhon', 'Doe', 'MALE', DATE '1998-12-12', 'doe@gmail.com' );
```
   **OR**


```SQL
INSERT INTO person ( first_name, last_name, gender, date_of_birth, email )
            VALUES ( 'Martin', 'Guptil', 'MALE', DATE '1890-8-30', 'guptil@gmail.com' );
```


Reading entries from Table 
```SQL
SELECT * FROM person;
```

Reading Specific Collum from Table
```SQL
SELECT first_name FROM person;
```


Reading multiple Collum from Table
```SQL 
SELECT first_name,email,id FROM person;
```


Generating Fake Data


Use [Mockaroo](https://www.mockaroo.com/) for generating random fake data


Create data in sql format then download in sql file. Then copy sql file in running postgres docker container.


Copy file to container using


`sudo docker cp /Downloads/person.sql post-app:/fs`


Open psql shell connecting to the database


Execute instructions from file in psql shell using 


`\i /path_to_file`


Hopefully you will see all comands executing and data added


Read data from person table and you will see your data


Organized Reading of Tables


```SQL
SELECT id,first_name,last_name,country FROM person ORDER BY country ASC;
```


   **OR**


```SQL
SELECT id,first_name,last_name,country FROM person ORDER BY country DESC;
```


Distinctive reading of table


```SQL
SELECT DISTINCT country FROM person;
```


Conditional reading using WHERE
```SQL
SELECT id,first_name,country FROM person WHERE country='Germany';
```
NOTE: It can also include comparisons like ` < > <= <> >= `


Multiple conditions using AND
```SQL
SELECT id,first_name,country,gender FROM person WHERE country='Canada' AND gender='Male';
```


Multiple conditions using OR
```SQL
SELECT id,first_name,country,gender FROM person WHERE country='Canada' OR country='Germany';
```


Combined Query
```SQL
SELECT id,first_name,country,gender 
FROM person WHERE country='Canada' 
OR country='Germany' 
ORDER BY id;
```


Mega Combined Query
```SQL
SELECT id,first_name,country,gender 
FROM person WHERE gender='Male' 
AND (country='Canada' OR country='Germany') 
ORDER BY id;
```


Limit number of results
```SQL
SELECT id,first_name,country FROM person LIMIT 10;
```


Combined mega pro query
```SQL
SELECT DISTINCT id,first_name,country,gender 
FROM person WHERE gender='Male' 
AND (country='Canada' OR country='Germany') 
ORDER BY id DESC 
LIMIT 3;
```


Offset results
```SQL
SELECT DISTINCT id,first_name,country,gender 
FROM person WHERE gender='Male' 
AND (country='Canada' OR country='Germany') 
ORDER BY id DESC 
OFFSET 1 
LIMIT 3;
```


Easier Check Using IN
```SQL
SELECT DISTINCT id,first_name,country FROM person WHERE country IN('Canada','Pakistan');
```


Range Reading Table using BETWEEN
```SQL
SELECT id,first_name FROM person WHERE id BETWEEN 10 AND 20;
```
 

***OR***
```SQL 
SELECT id,first_name FROM person WHERE date_of_birth BETWEEN DATE '1999-8-2' AND '2020-1-1';
```


Pattern search using LIKE & ILIKE
```SQL
SELECT id,email FROM person WHERE email LIKE '______@%';
```
***OR***
```SQL
SELECT id,email,country FROM person WHERE country ILIKE 'pak%';
```
NOTE: ILIKE is not case sensitive.


COUNT and GROUP BY
```SQL
SELECT country, COUNT(*) FROM person GROUP BY country;
```


Condititon on group results using HAVING
```SQL
SELECT country,COUNT(*) FROM person GROUP BY country HAVING COUNT(*) > 5 ORDER BY COUNT(*);
```


MAX function
```SQL
SELECT MAX(price) FROM cars;
```


MIN function
```SQL
SELECT MIN(id) FROM cars;
```


AVG function
```SQL
SELECT AVG(id) FROM cars;
```


Round function 
```SQL
SELECT ROUND(AVG(id),2) FROM cars;
```


Sum function
```SQL
SELECT SUM(id) FROM cars;
```


Arithimatic Operations
```SQL
SELECT id, ROUND(id * 0.10,2) FROM cars;
```


Alias using AS
```SQL
SELECT id, ROUND(id * 0.10,2) AS Ten_Percent FROM cars;
```


Default read using COALESCE
```SQL
SELECT COALESCE(email,'Undefined') FROM person;
```


Preventing 0 division by using NULLIF
```SQL
SELECT id / NULLIF(id,0) AS res FROM person;
```


Getting timestamp using NOW function
```SQL
SELECT NOW();
```


Casting timestamp to date
```SQL
SELECT NOW()::DATE;
```


Casting timestamp to time
```SQL
SELECT NOW()::TIME;
```


Date operations using INTERVAL
```SQL
SELECT NOW() - INTERVAL '1 YEAR';
```


Extracting parts from NOW function using EXTRACT function
```SQL
SELECT EXTRACT(CENTURY FROM NOW());
```


Altering constraints using ALTER TABLE
```SQL
ALTER TABLE person DROP CONSTRAINT person_pkey;
```


Deleting entry from table using DELETE
```SQL
DELETE FROM person WHERE id = 1;
```


Adding constraints using ALTER TABLE
```SQL
ALTER TABLE person ADD PRIMARY KEY(id);
```


Adding Constraints using ALTER TABLE;
```SQL
ALTER TABLE person ADD CONSTRAINT person_unique_email UNIQUE(email);
```


Add optional constraints using CHECK function
```SQL
ALTER TABLE person ADD CONSTRAINT gender_check CHECK( gender='Male' OR gender='Female');
```


***OR***


```SQL
ALTER TABLE person ADD CONSTRAINT id_check CHECK( id > 0 );
```


Delete all entries from table


```SQL
DELETE FROM cars;
```
