# Java Persistence API (JPA)

>Specification that defines standards for using `ORM (Object relational Mapping)` in Java application for interacting with a realitonal database.

`JPA` provides:
- API to map classes with tables
- API for performing CRUD operations
- `Java Persistence Query Language (JPQL)` 
    - query languages
    - for fetching data from database
- Criteria API
    -  uses object graph
    - to fetch data from database


## Entity Classes

- JPA provides annotations to create entity classes
- they are part of the `jakarta.persistence` package

Main annotations used:
- @Entity
- @Table
- @Id
- @Column

