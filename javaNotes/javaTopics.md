## Week 4 Assessment

### Database

A `database` is a SYSTEM of SOFTWARE and CAPABILITIES that make validating, storing, searching, filtering, aggregating, grouping, and administering data possible.

2 main categories

- `SQL`
- `NoSQL`

#### SQL Database

SQL databases are a type of RDBMS which use the standard Structured Query Language to administer the data. Data in a SQL database are started in objects called tables. Tables provide the relational information for the data stored in the database.

### RDBMS

_You will NOT be assessed on the details about the various vendors, any information after “Choosing Persistence”, nor about the Persistence Options activity_

- RDBMS manages data by storing them in tables.
- uses Structured Query Language (SQL)

### SQL Overview

Structured Query Language is the language used to administer SQL-based RDBM systems.

### Table

- Tables store and organize data in columns and rows as defined during table creation
- Tables are used to group the records in relation with each other and create a dataset.

### Sublanguage Overview

#### `DDL` - `Data Definition Language`

`DDL` sublanguage of SQL is utilized to create and manage the structure of a database.

- `CREATE`
  <br>The CREATE command is used to create objects on the server.
  - Database
  - Table
  - Index
  - Trigger
  - Function
  - Stored Procedure
  - View
- `DROP`
  <br>The DROP command is used to remove objects from the server. Any object created using the CREATE command can be dropped using the DROP command.
- `ALTER`
  <br>The ALTER command is used to change some characteristics of an object.
  - ADD / DROP columns
  - ADD / DROP constrains
  - Modify column data types
  - Modify column constrains
- `RENAME`
  <br>The RENAME command is used to rename objects
- `TRUNCATE`
  <br>The TRUNCATE command is used to remove all data from a table along with all space allocated for the records. Unlike DROP truncate will preserve the structure of the table.

```sql
-- create database
CREATE DATABASE IF NOT EXISTS mydb;
-- select database for current use
USE mydb;
-- create table
CREATE TABLE IF NOT EXISTS users (
  id INT SERIAL PRIMARY KEY,
  name VARCHAR(30)
);
-- alter table
ALTER TABLE users ADD CONSTRAIN name NOT NULL;
```

### Schema

- A database schema defines the structure of a database. Database schema is declared using a formal language, for RDBMS the language is SQL.
- An RDBMS schema can include objects like:
  - tables
  - triggers
  - functions
  - procedures
  - indexes
  - views
- In and RDBMS table the schema defines the columns, their data types, and constraints.

### SQL Datatypes

- Character types
  - Fixed-length
  - Variable-length
- Numeric types

  - Decimal

    - Decimal types are used to store exact fractional number values like money.
    - Types: decimal, float, double
    - The decimal data types decimal, float, double have a syntax that includes `type(p,s)`. In the syntax 'p' is the precision that represents the number of significant digits, 's' is the scale that represents the number of digits after the decimal point.

    ```sql
     annual_income decimal(10, 2)
    <!-- nnual_income will have a maximum of 10 digits with 8 before the decimal and 2 after it, with a max value of 99,999,999.99 -->
    ```

  - Integer
  - Floating point

- Temporal types
  - Date
  - Time
  - Timestamp

### Constraints

Constraints are used to define a database schema and are the backbone for defining `integrity constraints` of the schema. They help validate data beyond just a simple data type.

- `Not Null` Ensures that a column's value is not null.
- `Unique` Ensures that a column's value is unique in the table. (Can have one `NULL` value.)
- `Primary Key` Combines unique and not null. Uniquely identifies each row.
- `Foreign Key`` Links to a row in another table. Prevents the destruction of those links.
- `Default` Specifies a value for a column, if one is not given.
- `Check`
  - helps us to get only those values that are valid for the condition and our requirements.
  - ``
- `Create Index` Create a sorted index of the column for faster searching.

### Basic Queries

### Result Set

### DML

### DQL

### Aliases

### DROP vs TRUNCATE vs DELETE

### Intro to JDBC API

_Note: You will not be assessed over the Implementation section of this activity_

### DAO Design Pattern

### Using ResultSet

_Note: You will not be assessed over Callable Statements / Stored Procedures this week
Note: You will not be assessed over the Persisting Data with JDBC topic_
