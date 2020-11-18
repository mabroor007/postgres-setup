# postgres-setup-docker
This is a postgres setup on docker.
  Requirements:
         * Docker should be installed.
         * Basic Understanding of docker commands.
---
##Setup

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
`CREATE DATABASE test;`

### Step 6
Connect to a Database
 In psql shell type
    `\c name_of_database`
**Or**
 From Container Shell type
    `psql -h localhost -p 5432 -d test -U postgres`

### Step 7
Deleting a database
`DROP DATABASE name_of_database;`
CareFull its Dangerous.

### Step 8
Exiting psql shell
`\q`


## Usage 

###CHEAT SHEAT
| Command | Functionality |
|---|------|
| \l | List of all the databases |
| \d | List of all the Tables in Current database |
