## Database Intro

A `database` is a SYSTEM of SOFTWARE and CAPABILITIES that make validating, storing, searching, filtering, aggregating, grouping, and administering data possible.

2 main categories

- `SQL`
- `NoSQL`

### RDBMS

> What is a RDBMS?

An RDBMS is a data storage system based on a relational model

- RDBMS manages data by storing them in tables.
- uses Structured Query Language (SQL)

### SQL Database

> What is SQL and why would we use this language

`Structured Query Language` (`SQL`) is the language used to administer SQL-based RDBM systems.

SQL databases are a type of RDBMS which use the standard Structured Query Language to administer the data. Data in a SQL database are stored in objects called tables. Tables provide the relational information for the data stored in the database.

### Schema

- A database schema defines the structure of a database. Database schema is declared using a formal language, for RDBMS the language is SQL.
- An RDBMS schema can include objects like:
  - tables
  - triggers
  - functions
  - procedures
  - indexes
  - views
- In an RDBMS table the schema defines the columns, their data types, and constraints.

#### Table

> Describe relational database tables.

In MySQL, a table stores and organizes data in columns and rows as defined during table creation.

- a `row` in a table represents a relationship among a set of values

TABLE commands:

- `CREATE TABLE`
- `DROP TABLE`
- `TRUNCATE TABLE`
- `ALTER TABLE`

Create Table Example
```sql
CREATE TABLE Departments (
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(50)
);

CREATE TABLE Employees (
    ID INT PRIMARY KEY,
    FirstName VARCHAR(50),
    LastName VARCHAR(50),
    Email VARCHAR(100),
    DeptID INT,
    FOREIGN KEY (DeptID) REFERENCES Departments(DeptID)
);
```

Alter Table Examples
```sql
-- add column
ALTER TABLE Employees
ADD BirthDate DATE;

-- modify column
ALTER TABLE Employees
MODIFY COLUMN Email VARCHAR(200);

-- delete column
ALTER TABLE Employees
DROP COLUMN BirthDate;
```
#### View

> What is a view and why is it useful?

In `MySQL`, a `View` is a virtual table based on the result-set of an SQL statement. A view consists of rows and columns, just like a common table. The view fields are fields from one or more real tables in the database.

Advantages:

- Structure data in a way that users or classes of users find natural or intuitive.
- Restrict access to the data in such a way that a user can see and manipulate exactly what they need.
- Summarize data from various tables which can be used to generate documents and reports.

```sql
CREATE VIEW view_name AS
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```

#### Index

> What is an index in SQL?

- a database structure that improves the performance of queries on a table
- created on one or more columns and stores sorted copy of data in those columns
- when a query is executed on columns, database can use index for finding data quickly

##### Index Syntax

```sql
-- create index
CREATE UNIQUE INDEX index_name ON table_name ( column1, column2,...);
CREATE UNIQUE INDEX EMPINDEX ON EMPLOYEE (EMPID)

-- add index to an existing table
ALTER TABLE testalter_tbl ADD INDEX (c);

-- drop index from an existing table
ALTER TABLE testalter_tbl DROP INDEX (c);
```

### Constraints

> What are constraints and can you describe a few constraints?

`Constraints` are rules for columns to ensure validity of data. They are used to restrict the values of data which are inserted into a table.

`Constraints` are used to define a database schema and are the backbone for defining `integrity constraints` of the schema. They help validate data beyond just a simple data type.

- `NOT NULL` Ensures that a column's value is not null.
- `UNIQUE` Ensures that a column's value is unique in the table. (Can have one `NULL` value.)
- `PRIMARY KEY` Combines unique and not null. Uniquely identifies each row.
- `FOREIGN KEY` Links to a row in another table. Prevents the destruction of those links.
- `DEFAULT` Specifies a value for a column, if one is not given.
- `CHECK`
  - helps us to get only those values that are valid for the condition and our requirements.
- `CREATE INDEX` Create a sorted index of the column for faster searching.

```sql
create table content_meta (
	id int auto_increment primary key,
    content_type int not null,
    url varchar(500) not null unique,
    uploader int not null,
    size_in_bytes bigint default 1,
    uploaded_at timestamp default now(),
    constraint url_scheme_check check(instr(url, 'http://') > 0),
    constraint size_check check(size_in_bytes > 0), check(size_in_bytes < 10000000),
    foreign key(content_type) references content_type(id),
    foreign key(uploader) references users(id),
    index (content_type)
);
```

### Composite Key

`Composite Key` is combining two or more keys in a table to create a primary key to uniquly identify a record.

`Compound Key` is a `Composite Key` where each attribute creating a key is a `Foreign Key`.

### Foreign Key

> What is a foreign key?

A `FOREIGN KEY` is a field or collection of fields in a table that refers to the `PRIMARY KEY` of the other table.

- responsible for managing the relationship between the tables.
- forms the bases of referential integrity

```sql
CREATE TABLE Branch(
    branch_id INT PRIMARY KEY,
    branch_name VARCHAR(20)
     );
-- Add branch_id as foreign key for employee table

ALTER TABLE employee ADD branch_id INT;
ALTER TABLE employee ADD FOREIGN KEY (branch_id) REFERENCES Branch(branch_id);
```

### Referential Integrity

> What is referential integrity?

`REFERENTIAL INTEGRITY` is the relationship between tables.

Referential Integrity:

- the requirement that a foreign key cannot be defined unless its corresponding primary key exists is a referential integrity constraint
- does not allow the addition of any record in a table that contains the foreign key unless the reference table contains a corresponding primary key.
- does not allow to deletion of a record in a table that contains the foreign key, to delete the record in the parent table, the corresponding record in the child table should be deleted first. to solve this issue `ON DELETE CASCADE` is used.
- Other options are to set the foreign key to null or to its default value (only if the default value references an existing value in the primary-key table).

### Normalization

> What is normalization?

`Normalization` is the process of organizing the data and the attributes of a database.

- reduce the duplication of data, - avoid data anomalies
- ensure referential integrity
- simplify data management

- `1NF` First Normal Form

  - Each table cell should contain a single value.
  - Each record needs to be unique
  - violation example: hobbies with several values
  - solution add new rows with each value

- `2NF` Second Normal Form

  - Be in 1NF
  - Single Column Primary Key - that does not functionally dependant on any subset of candidate key relation
  - violation example: name and address identifies a record when two different people have the same name
  - solution: add a primary key column

- `3NF` Third Normal Form

  - in 2NF
  - all the attributes (e.g. database columns) are functionally dependent on solely the primary key (no transitive functional dependencies)
  - violation example: hospital database having a table of patients which included a column for the telephone number of their doctor. The phone number is dependent on the doctor, rather than the patient, thus would be better stored in a table of doctors
  - solution: create table for doctors and store phone number there

- BCNF Boyce-Codd Normal Form
  - in 3NF
  - for any dependency A → B, A should be a super key. which means that A should be a non-key attribute if B is a key attribute
  - for every Functional Dependency, LHS is the super key - ???????????????
  - no dependency and lossless join - ??????????????????

### Multiplicity

> What is multiplicity?

`Multiplicity` defines the relationship between two tables

There are 4 different multiplicity relationships

- one to one
  - implementation: the table that references the other table must have a foreign key column to the referenced table. This column must have a UNIQUE constraint applied to it.
  - example: student - backpack
- one to many
  - implementation: the "many" table would have a foreign key to the "one" table
  - example: albums - songs
- many to one
  - same as one to many
- many to many
  - implementation: a third table needs to be created (called a junction table) that has a foreign key to both tables
  - example: doctor -patient

## SQL Language Intro

### SQL Datatypes

The purpose of SQL data types is to constraint a columns expected value.

- Character types
  - Fixed-length - `MY_VALUE CHARACTER(10)`
    - size: 10 bytes
  - Variable-length - `MY_VALUE VARCHAR(255)`
    - size: min 2 bytes, max 255 bytes
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

- Boolean
- Temporal types
  - Date
  - Time
  - Timestamp

### SQL Operators

> What are some operators that can be used in SQL?

- Arithmetic (`+`, `-`, `*`,`/`,`%`)
- Bitwise (`&`, `|`, `^`)
- Comparison (`=`, `<`, `>`, `>=`, `<=`, `<>`)
- Compound (`+=`, `-=`, ...)
- Logical
  - `ALL` - TRUE if all of the subquery values meet the condition
  - `AND` - TRUE if all the conditions separated by AND is TRUE
  - `ANY` - TRUE if any of the subquery values meet the condition
  - `BETWEEN` - TRUE if the operand is within the range of comparisons
  - `EXISTS` - TRUE if the subquery returns one or more records
  - `IN` - TRUE if the operand is equal to one of a list of expressions
  - `LIKE` - TRUE if the operand matches a pattern
  - `NOT` - Displays a record if the condition(s) is NOT TRUE
  - `OR` TRUE if any of the conditions separated by OR is TRUE
  - `SOME` TRUE if any of the subquery values meet the condition

### SQL Sublanguages

- DDL - Data Definition Language
- DML - Data Management Language
- DCL
- TTL
- DQL

## SQL `DDL` - `Data Definition Language`

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

## SQL `DML` Data Manipulation Language

- `INSERT`
- `UPDATE`
- `DELETE`

```sql
INSERT INTO Employees (ID, FirstName, LastName, Email)
VALUES (1, 'John', 'Doe', 'john.doe@example.com');

UPDATE Employees
SET Email = 'j.doe@example.com'
WHERE ID = 1;

DELETE FROM Employees
WHERE ID = 1;
```

## DCL - Data Control Language

> What is DCL?

The `Data Control Language` (`DCL`) of SQL is used to control rights, and permissions of users on database objects.

The DBA (DataBase Administrator) would be responsible to setup user (application) access prior to the user attempting to login to the database.

- `GRANT` - grant privilege
- `REVOKE` - remove privilege

### Privileges

A database can have numerous privileges which can be permitted to users. Most common ones:

- `Select` - allows select statements on tables
- `Insert` - allows insert statements on tables
- `Delete` - allows delete statements on tables
- `Update` - allows update statements on tables
- `Index` - allows creating indexes on tables
- `Create` - allows create table statements
- `Alter` - allows alter table statements
- `Drop` - allows drop table statements
- `All` - allow all permissions except grant
- `Grant` - allows grant statements

### Syntax

```sql
GRANT <privileges> ON <object> TO <user>;
-- GRANT all CRUD ablities to user
GRANT SELECT, INSERT, UPDATE, DELETE ON employees TO 'john';

REVOKE <privileges> ON <object> FROM <user>;
```

## SQL TCL - Transaction Control Language

> What is TCL?

TCL commands help the user manage the transactions that take place in a database.

- a `transaction` is a set of SQL statements that are executed on the data stored in DBMS
- Whenever we perform any of the DDL command like -INSERT, DELETE or UPDATE, these can be rollback if the data is not stored permanently
- to make the changes permanent, we use TCL commands
- TCL commands are used to ensure the transaction satisfies all the ACID properties

### SQL Transaction

> What is a transaction?

- transaction: one or more DQL or DML operations performed on a database as a single unit
- DDL can be included, but cannot be rolled back. Don't use DDL in a transaction mixed with other statements
- desirable transaction properties:
  - **A**TOMICITY: either all statements succeed or they all fail
  - **C**ONSISTENTENCY: transactions keep data in a consistent state
  - **I**SOLATION: ability of transactions to not interfere with one another (isolation level can be changed)
  - **D**URABILITY: transactions are logged, saved to long-term memory, and are recoverable
- there are only two outputs for a transaction, success or failure, if all the statements are executed successfully the transaction is successful, even if a single statement fails, the entire transaction fails.

### TCL Commands

- `START TRANSACTION` - notifies MySQL that the statements after Start should be cosidered as a single unit.
- `COMMIT` - used to save the data permanently
- `ROLLBACK` - used to get the data or restore the data to the last savepoint or last committed state
- `SAVEPOINT` - used to save the data at a particular point temporarily

### Example

```sql
START TRANSACTION;
INSERT INTO bankaccounts VALUES("ACC3", 10000);
SAVEPOINT sv;
INSERT INTO bankaccounts VALUES("ACC4", 900000);
ROLLBACK TO sv;
INSERT INTO bankaccounts VALUES("ACC4", 90000);
COMMIT;

-- BANK TRANSER TRANSACTION
START TRANSACTION or BEGIN; --statement1
UPDATE bankaccounts SET funds=funds-100 WHERE account_no='ACC1'; --statement2
UPDATE bankaccounts SET funds=funds+100 WHERE account_no='ACC2'; --statement3
COMMIT; --statement4
```

### Transaction Properties (`ACID`)

> What are the properties of a transaction?

- `Atomicity` - is combining all statements into a single unit. A transaction is considered to be atomic if it cannot be further broken down into individual operations and, all of the operations that occur within a transaction either succeed or fail as a single unit. If a single operation fails during a transaction, then everything is considered to have failed and must be rolled back.

- `Consistency` : One of the advantages of using a transaction is that, even if the transaction is a success or a failure, the database is consistent and the data integrity is maintained.
  All inconsistent data is removed, and all transactions that might cause inconsistency are aborted and an error is created or transcribed into an error log. Example: Consider two bank accounts ACC1 and ACC2 with funds of 10000$ and 9000, which is is total of 19000, after a transaction of transferring 50$ from ACC2 to ACC1 the funds in ACC1 is 10050$ and ACC2 are 8950$, which means the totals funds in AC1 and ACC2 adds up to 19000, So the funds in ACC1 and ACC2 are consistent before and after the Transaction.
- `Isolation`: Every transaction is isolated from other transactions. Therefore, a transaction shouldn't affect other transactions running at the same time. Stated another way, data modifications made by one transaction should be isolated from the data modifications made by other transactions. So, while a transaction can see data in the state it was in before another concurrent transaction modified it, as well as after the second transaction has completed, it cannot see any intermediate states. Example: Consider that the user A withdraws $100 and user B withdraws $250 from user ACC1 account, which has a balance of $1,000. Since both A and B draw from ACC1 account, one of the users is required to wait until the other user transaction is completed, avoiding inconsistent data.

- `Durability`:
  Transactions help with Durability in a few ways: data modifications that take place within a successful transaction may be safely considered to be stored in the database regardless of whatever else may occur. As each transaction is completed, a row is entered in the database transaction log. Thus, in the event of a system failure that requires the database to be restored from a backup you can use this transaction log to get the database back to the state it was in after a successful transaction.

  - once these transactions are successfully executed, the changes made to the database are permanent even if an unexpected system failure or an error occurs.

  The ACID property of DBMS plays a vital role in maintaining the consistency and availability of data in the database

#### Transaction Isolation Levels (Supplementary)

- read uncommitted: transactions can read uncommitted changes made by others (dirty reads)
- read committed: selecting same data multiple times in a transaction and not getting the same information (nonrepeatable read) as other transactions commit modifications
- repeatable read: uses data in its state at the start of a transaction, prevents nonrepeatable read / updates to the data being read
- serializable: ensures, while a transaction is reading data, thatno data is removed or deleted that can cause a difference (phantom reads)

### DML

The `DML` (`Data Management Language`) sublanguage of SQL is utilized to create, update, and delete data in a database.

- `INSERT`
- `UPDATE`
- `DELETE`

```sql
INSERT INTO roles (id, name) values (1, 'ADMIN'), (2, 'OWNER'), (3, 'EDITOR'), (4, 'VIEWER');

UPDATE permissions set categoryId=1;

DELETE FROM roles where name='VIEWER';
```

### DROP vs TRUNCATE vs DELETE

<table>
<thead><td>DELETE</td><td>TRUNCATE</td><td>DROP</td></thead>
<tbody>
<tr>
<td>DML</td><td>DDL</td><td>DDL</td>
</tr>
<tr>
<td>WHERE clause can be used to filter and delete one or more rows</td>
<td>WHERE clause cannot be used</td>
<td>WHERE clause cannot be used</td>
</tr>
<tr>
<td>It is executed using <strong>row lock</strong>, and each row in the table is locked for deletion</td>
<td>It is executed using <strong>table lock</strong>, where whole table is locked while removing the records</td>
<td>It removes a table form the database</td>
</tr>
<tr>
<td>It maintains the log, so it is slower than TRUNCATE</td>
<td>Least amount of logging needed so it is faster in performace</td>
<td>It maintains the log, so it is slower than TRUNCATE</td>
</tr>
<tr>
<td>It can roll back the deleted data before committing it</td>
<td>It cannot be rolled back</td>
<td>It cannot be rolled back</td>
</tr>
</tbody>
</table>

## SQL DQL

`DQL` the `Data Query Language` is used to search, filter, group and aggregate stored data

- uses the `SELECT` statement
- retrieves a `Resultset`

```sql
SELECT [ALL | DISTINCT]
    select_expr [, select_expr] ...
    [into_option]
    [FROM table_ref]
    [WHERE where_condition]
    [GROUP BY {col_name | expr | position}]
    [HAVING having_condition]
    [ORDER BY {col_name | expr | position}]
        [ASC | DESC]
    [LIMIT {[offset,] row_count | row_count OFFSET offset}];

```

### Clauses

#### `WHERE` Clause

`WHERE` filters and extracts only records that match condition

- if using an aggregate function, WHERE filters before it is called
- `HAVING` is used only if an aggregate function is called
- HAVING filters after the function call

> Why would I use the WHERE clause?

The `WHERE` clause is not only used in `SELECT` statements, it is also used in `UPDATE`, `DELETE` as well

FILTERING: The filtering clause of a select statement is a `WHERE` clauses that defines how selected rows are filtered from the table.

##### WHERE Clause Operators

WHERE` clauses use to select records that meet specific conditions:

- logical operators
- comparison operators
- matching operators

Operators:

- `AND` true if both boolean expresions evaluate to true
- `IN` true if the operand is included in a list of expressions
- `NOT` Reverses the value of any boolean expression
- `OR` true if either or both boolean expressions is true
- `LIKE` true if the operand matches a pattern
  - `%` (percent) match any string of zero or more characters
  - `_` (underscore) match any single character
- `BETWEEN` true if the operand falls within a range
  Where Logical operators

#### `GROUP BY` Clause

> What is the GROUP BY clause used for?-

- used to group data based on the exact value in a specific field
- groups rows that have the same values into summary rows
- have to be used with aggregate functions like `COUNT`, `MAX`, `MIN`.

#### `HAVING` clause
> Used to filter the results of an aggregate function.

```sql
SELECT DeptID, COUNT(ID) as EmployeeCount
FROM Employees
GROUP BY DeptID
HAVING COUNT(ID) > 5;
```

#### `ORDER BY` Clause

> What is the ORDER BY clause used for?

- `ORDER BY` clause is used to sort the returned records by a specified column
- The records can be ordered either `ASC` (ascending) or `DESC` (descending).
- Ascending order is default if not specified.

### Other Clauses

- `LIMIT` clause restricts number of records returned from the select statement.
- `OFFSET` clause specifies from which record position to start counting from. This is often used in conjunction with the `LIMIT` clause. NOTE: Some SQL implementations use the `SKIP` keyword instead of offset

### Aliases

Aliases is used to give a temporary name to a table or a column in a table for the intention to support a specific query.

```sql
SELECT column_name AS alias_name FROM table_name;
```

Advantages:

- It provides a very useful feature that allows us to achieve complex tasks quickly.
- It makes column or table name more readable.
- It allows us to combine two or more columns
- It makes the table more user-friendly.

## SQL Joins

> Describe what a join is and explain the different types of joins we can create.

#### Inner

`INNER JOIN` restricts records retrieval from Table1 and Table2 to those that satisfy the join requirement.

#### Left

`LEFT JOIN` returns all records from the left table, and the records that match the condition from the right table.

#### Right

`RIGHT JOIN` returns all records from the right table, and the records that match the condition from the left table.

#### Cross

`MySQL` `CROSS JOIN`, commonly knows as a `CARTESIAN JOIN`, returns all possible row combinations from each table.

If no other condition is provided, the result set is obtained by multiplying each row of table1 with all rows in table2.

If there is a relationship between two tables and we add a WHERE clause, then the CROSS JOIN will produce the same result as INNER JOIN.

Real world application includes calculating all possibilities when launching a space rocket.

#### Self

`SELF JOIN` is an SQL statement which is used to intersect or join a table in the database to itself.

## SQL Set Operations

> What is the difference between a join and a set operation?

SET Operators are specific type of operators which are used to combine the result of two queries.

#### UNION

The `UNION` command is used to combine more than one SELECT query results into a single query contain rows from all the select queries.

- The number of columns and data types in the SELECT statements must be the same in order for the UNION command to work.
- `MySQL` uses the `DISTINCT` clause as the default when executing UNION

#### UNION ALL

The `UNION ALL` clause is used to display all even the duplicate rows in UNION query.

#### INTERSECT

The `INTERSECT` clause is used to display all records which are common between two tables.

#### MINUS

The `MINUS` clause ( also called as `EXCEPT` clause in some books) is used to display the records from table 1 while removing the records which are also present in table 2.

## SQL Functions & Procedures

Must have `CREATE ROUTINE` privilige to create stored functions and stored procedures on the database.

> What is a function in SQL?

A function in MySQL is a set of statements you can call by name.

- callable block of code that takes in zero or more parameters and returns a value
- mainly used to perform and return calculations
- must RETURN value
- can be used as part of a SQL expression (since it returns a value)
- can include DQL and DML (and DDL but not used often in function)
- some are built-in and we can create our own
- to use a function use `SELECT`: `SELECT COUNT(*)...`
- Stored functions are very similar to stored procedures, except that a function returns a value to the environment in which it is called.

> What is the difference between an aggregate and a scalar function?

- A scalar function is a function that operates on scalar values. It takes one (or more) input values as arguments directly and returns a value.
- An aggregate function is a function that operates on aggregate data. It takes a complete set of data as input and returns a value that is computed from all the values in the set.

### Aggregate Functions

- functions that return one value from one or more records
- MySQL aggregate functions retrieve a single value after performing a calculation on a set of values.
- In general, aggregate functions ignore null values.
- `GROUP BY` and `HAVING` are used with aggregate functions, they group records based on the column values

Most important aggregate functions:

- `count()` - Returns the number of rows, including rows with NULL values in a group.
- `sum()` - Returns the total summed values in a set. -`average()` - Returns the average value of an expression.
- `min()` - Returns the minimum (lowest) value in a set.
- `max()` - Returns the maximum (highest) value in a set.

```sql
SELECT MIN(salary) FROM employee;
```

### Scalar Functions

Functions that return a value for every record.

Scalar functions are pre-defined functions in SQL, and whatever be the input provided to the scalar functions, the output returned by these functions will always be a single value.

Most important scalar functions:

- `UCASE()` - Converts the value of a field to uppercase.
- `LCASE()` - Converts the value of a field to lowercase.
- `MID(string, start, end)` - returns substring
- `LENGTH()` - Returns the length of the value in a text field.
- `ROUND(NumericalValue, Decimals)`
- `NOW()` - Returns the current system date and time.
- `FORMAT(Value, Decimal)`

```sql
SELECT MID ("Hello World", 4, 8) AS Substring;
-- returns:"lo World"

SELECT ROUND (NumericValue, Decimals);

SELECT ROUND (1560.44444, 2) AS Round_Value;
-- returns: 1560.44

SELECT FORMAT (1234.1234, 2) AS Format_Number;
-- returns: 1234.12
```

### Stored MySQL Functions

Characteristics of a function include:

- Functions are separate block that is mainly used for calculation purpose.
- Function with DML commands can be called from other MySQL blocks, but function without DML commands can be directly called in SELECT query.
- The values can be passed into the function or fetched from the procedure through the parameters.
- These parameters should be included in the calling statements.
- A function uses RETURN command to return the value or raise the exception, i.e. return is mandatory in functions.
- As it will always return the value, in calling statements it always accompanies with assignment operator to populate the variables.

#### Syntax

```sql
-- FUNCTION CREATION
CREATE FUNCTION function_name [ (parameter datatype [, parameter datatype]) ] RETURNS return_datatype

BEGIN

declaration_section

executable_section

END;

-- FUNCTION EXECUTION
SELECT function_name(parameters);

-- FUNCTION DELETION
DROP FUNCTION [ IF EXISTS ] function_name;
```

#### Example

```sql
-- create
CREATE FUNCTION get_balance(acc_no INT) RETURNS INT

BEGIN
  SELECT order_total
  INTO acc_bal
  FROM orders
  WHERE customer_id = acc_no;
  RETURN(acc_bal);
END;

-- execute
SELECT get_balance(101);

-- delete
DROP FUNCTION IF EXISTS get_balance;
```

### Triggers

> What is a trigger in SQL?

A trigger is a named SQL unit that is stored in the database and run in response to an event that occurs in the database or when there is a modification to the database.

- database object that activates when a particular event occurs on the table it is associated with
- a special kind of a store procedure that executes in response to certain action on the table like insertion, deletion or updation of data
- events are DML (insert, delete, update)
- You can specify the event, whether the trigger fires before or after the event, and whether the trigger runs for each event or for each row affected by the event.

The key difference between a `trigger` and `procedure`:

- a trigger is _called automatically_ when a data modification occurs in a table. A stored procedure must be invoked directly.
- Triggers have no chance of recieving parameters.
- A transaction cannot be committed or rolled back inside a trigger.

#### Types of Triggers:

- AFTER INSERT activated after data is inserted into the table.
- AFTER UPDATE: activated after data in the table is modified.
- AFTER DELETE: activated after data is deleted/removed from the table.
- BEFORE INSERT: activated before data is inserted into the table.
- BEFORE UPDATE: activated before data in the table is modified.
- BEFORE DELETE: activated before data is deleted/removed from the table.

#### Trigger Syntax

```sql
-- create trigger
CREATE TRIGGER [trigger_name] [BEFORE | AFTER]
{INSERT | UPDATE | DELETE}
ON [table_name]
[for each row]
[trigger_body]

-- delete trigger
DROP TRIGGER [IF EXISTS] trigger_name
```

Example:

```sql
CREATE TRIGGER student_grade
BEFORE INSERT
ON Student
for each row
SET Student.total = Student.subj1 + Student.subj2 + Student.subj3, Student.perc = Student.total * 50 / 100;
```

### Stored Procedures

> What is a stored procedure in SQL?

A stored procedure is a MySQL program that is stored inside a database schema and which can be invoked from within a MySQL program or SQL command.

- callable block of code that takes in parameters
- does not use a return statement
- can include DQL and DML (and DDL but not used often in function)
- can contain TCL
- `CallableStatement` is used in Java to call a stored procedure

- A stored procedure provides additional layer of security between the user interface and the database.
- It supports security through data access controls because end users may manipulate data, but doesn't write procedures.
- It offers advantages over embedding queries in a graphical user interface.

#### Stored Procedures vs. Functions

- Stored procedures and functions can be used to accomplish the same task.
- Both can be user-defined as part of any application,
- functions are defined to send their output to a query
- Stored procedures are designed to return outputs to the application
- a user-defined function returns table variables and cannot change the server environment or operating system environment.

### Procedure Parameters

- `IN`: input parameter. default (and only) type for functions. works like Java parameters (value is used but modifications do not modify original value/variable itself)
- `OUT`: value from procedure is passed to caller. user defined variable needed.
- `INOUT`: caller passes in value and CAN be modified by procedure and modification is reflected outside of procedure. user defined variable needed.

#### Stored Procedure Syntax

```sql
-- create procedure
CREATE PROCEDURE procedure_name ( IN | OUT | INOUT parameter_name parameter_datatype (length), … )
BEGIN
SQL statements
END//

--  execute procedure
CALL stored_procedure_name([IN parameter],@[OUT parameter]);

-- drop procedure
DROP PROCEDURE [IF EXISTS] stored_procedure_name;
```

Example:

```sql
-- Example 1
-- create:
CREATE PROCEDURE get_product( IN prod_id int )
BEGIN
SELECT * FROM products WHERE product_id = prod_id; END //
-- execute
CALL get_product(1);
-- result
-- product_id	product_name	cost
-- 101	iPhone	450


-- Example 2 :
-- create
CREATE PROCEDURE get_count( IN prod_id int, OUT total INT )
BEGIN
SELECT COUNT(*) INTO total FROM products WHERE product_id = prod_id;
END //
-- execute
call get_count(4,@total);
select @total;
-- result
-- @total
-- 4


-- Example 3 :
-- create
CREATE PROCEDURE counter( INOUT count INT, IN increment INT )
BEGIN
SET count = count + increment;
END //
-- execute
SET @count = 5;
call counter(@count, 2);
select @count;
-- result
-- @count
-- 7
```

### Sequence (Not Creatable in MySQL)

A sequence is a user-defined schema bound object that produces a sequence of numeric values.

- database object that generates a series of integer values
- starting value must be positive
- increment can be custom

The `AUTO_INCREMENT` column attribute provides unique numbers in MySQL.

- AUTO_INCREMENT sequences start with 1 by default
- only one column per table can have this attribute

#### Sequence Syntax

```sql
CREATE SEQUENCE schema_name.sequence_name [OR] sequence_name
START WITH initial_value
INCREMENT BY increment_value
MINVALUE min_value
MAXVALUE max_value
CYCLE|NOCYCLE ;
```

- sequence_name: Name of the sequence.

- initial_value: starting value from where the sequence starts. Initial_value should be greater than or equal to minimum value and less than equal to maximum value.

- increment_value: Value by which sequence will increment itself. Increment_value can be positive or negative.

- minimum_value: Minimum value of the sequence.

- maximum_value: Maximum value of the sequence.

- cycle: When sequence reaches its set_limit it starts from beginning.

- nocycle: An exception will be thrown if sequence exceeds its max_value.

Example

```sql
CREATE SEQUENCE example_1 AS INT START WITH 10 INCREMENT BY 10;

CREATE SEQUENCE example_2 start with 100 increment by -1 minvalue 1 maxvalue 100 cycle;
```

### Flow Control Statements (Supplementary)

- https://dev.mysql.com/doc/refman/8.0/en/flow-control-statements.html
