# postgres-setup-docker
This is a postgres setup on docker.
  Requirements:
         * Docker should be installed.
         * Basic Understanding of docker commands.

# --------------------------------(Setup)----------------------------------

# STEP 1
Pull latest postgres alpine image from docker hub.

# STEP 2
use following command to run Postgres Container
"""docker run -d --name my-db-server -p 5432:5432 -e POSTGRES_PASSWORD=pwd postgres:alpine"""

# STEP 3
Open container shell by following command
"""docker exec -it my-db-server bash"""

# STEP 4
Open psql shell by this command
"""psql -U postgres"""

# STEP 5
Create a Database
"""CREATE DATABASE test;"""

# STEP 6
Connect to a Database
 :In psql shell type
    """\c name_of_database"""
Or
 :From Container Shell type
    """psql -h localhost -p 5432 -d test -U postgres"""

# STEP 7
Deleting a database
"""DROP DATABASE name_of_database;"""
CareFull its Dangerous.

# STEP 8
Exiting psql shell 
"""\q"""

# ----------------------------(Setup finished)-----------------------------

# Usage 

List of all the databases """\l""" \n
List of all the tables in current database """\d""" \n
