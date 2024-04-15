# [Spring](https://spring.io)

- makes developing in java faster, simple
- responding to http requests
- conecting to database
## To Start Spring App

### [Initialize App](https://start.spring.io/)

#### 1. Set Configuration:
- Project: `Maven`
- Language: `Java`
- Spring Boot: `3.2.4`, do not select SNAPSHOTS
- Project Metadata:
    - Group: com.werner
    - Artifact: MyAPp
    - Name: same as artifact
    - Description: as needed
    - Packaging: `Jar`
- Dependencies:
    - `Spring Web` for handling `HTTP Requests` 
    - `Spring Data JPA` for handling a database
    - `PostgreSQL Driver` for postgreSQL database

#### 2. Generate App
- Click the `Generate`
- Extract downloaded `zip` file



## Set Up DBeaver
### Create Database Connection
- click on `plug with + sign icon` in the upper left corner under `File`
- select the `Postgres` icon
- select the `Next` button
- set configuraton
    - `Host` should remain `localhost`
    - enter password
- test connection with the `Test Connection` button
- click the `Finish` button

### Find Schema to Connect to in Spring Boot MVC APp
- Open the `postgres-localhost` connection we just created
- keep opening until you hit `Schemas` postgres -> Databases -> postgres -> Schemas
- under `Schemas` the `public` is the default schema we will use

### To delete a connection
- `Projects -> General -> Connections`
- select connection to delet
- select delete form mouse menu


## Configuration Database in Spring Boot App

With the configuration below we set what database our app will use.

`src/main/resources/application.properties`
```bash

# Database Credentials (we need these to connect to our database)------------------------

spring.datasource.url=jdbc:postgresql://localhost:5432/postgres
spring.datasource.username=postgres
spring.datasource.password=password

# Spring Data Settings  -----------------------

# This allows us to see SQL running in the console - great for debugging
spring.jpa.show-sql=true

# Setting our DDL to update when a change happens (creation/updates)
spring.jpa.hibernate.ddl-auto=update
# We could have set this to "create" to drop and recreate the database each time

# Specify what DB schema we're pointing to
spring.jpa.properties.hibernate.default_schema=public
```




