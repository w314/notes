
oracle, db, sql, constraint

 

# Constraints

- single column

- composite - table level

 

## NOT NULL

- can only be applied as a `Column Level Constraint`

```sql

CREATE TABLE Users (

    UserName VARCHAR(100) CONSTRAINT user_Uname_nn NOT NULL

);

```

 

## DEFAULT

 

- data type of column must be the same as the data type of the default expression

- can be provided for both `nullable` and `NOT NULL` attributes

- **Oracle** does does **not** consider it as a **constraint**

```sql

CREATE TABLE Services (

    ServiceDate DATE DEFAULT SYSDATE

);

```

 

## PRIMARY KEY

- does **not** allow `NUll` values or duplicates

- we can have only one primary key per table

```sql

CREATE TABLE Dogs (

    DogId INTEGER CONSTRAINT dog_dId_pk PRIMARY KEY

);

```

 

