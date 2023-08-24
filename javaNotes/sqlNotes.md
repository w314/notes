## SQL

> What is SQL and why would we use this language

`Structured Query Language` (`SQL`) is the language used to administer SQL-based RDBM systems.

## Database

A `database` is a SYSTEM of SOFTWARE and CAPABILITIES that make validating, storing, searching, filtering, aggregating, grouping, and administering data possible.

2 main categories

- `SQL`
- `NoSQL`

#### SQL Database

SQL databases are a type of RDBMS which use the standard Structured Query Language to administer the data. Data in a SQL database are stored in objects called tables. Tables provide the relational information for the data stored in the database.

### RDBMS

> What is a RDBMS?

An RDBMS is a data storage system based on a relational model

- RDBMS manages data by storing them in tables.
- uses Structured Query Language (SQL)

- RDBMS manages data by storing them in tables.
- uses Structured Query Language (SQL)

### SQL Overview

Structured Query Language is the language used to administer SQL-based RDBM systems.

### Table

> Describe relational database tables.

In MySQL, a table stores and organizes data in columns and rows as defined during table creation.

- Tables are used to group the records in relation with each other and create a dataset.

TABLE commands:

- `CREATE TABLE`
- `DROP TABLE`
- `TRUNCATE TABLE`
- `ALTER TABLE`

### View

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

#### `DML` Data Manipulation Language

- `INSERT`
- `UPDATE`
- `DELETE`

#### DCL - Data Control Language

> What is DCL?

The `Data Control Language` (`DCL`) of SQL is used to control rights, and permissions of users on database objects.

The DBA (DataBase Administrator) would be responsible to setup user (application) access prior to the user attempting to login to the database.

- `GRANT` - grant privilege
- `REVOKE` - remove privilege

##### Privileges

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

##### Sytax

```sql
GRANT <privileges> ON <object> TO <user>;
-- GRANT all CRUD ablities to user
GRANT SELECT, INSERT, UPDATE, DELETE ON employees TO 'john';

REVOKE <privileges> ON <object> FROM <user>;
```

#### TCL - Transaction Control Language

> What is TCL?

TCL commands help the user manage the transactions that take place in a database.

- a `transaction` is a set of SQL statements that are executed on the data stored in DBMS
- Whenever we perform any of the DDL command like -INSERT, DELETE or UPDATE, these can be rollback if the data is not stored permanently
- to make the changes permanent, we use TCL commands
- TCL commands are used to ensure the transaction satisfies all the ACID properties

##### Transaction

> What is a transaction?

- In SQL transaction is grouping of statements into a single unit.
- A transaction satisfies all the ACID properties.
- In MySQL, transactions are SQL statements that are grouped under a single unit, the statements in a transaction will then be executed one by one
- there are only two outputs for a transaction, success or failure, if all the statements are executed successfully the transaction is successful, even if a single statement fails, the entire transaction fails.

##### TCL Commands

- `START` - notifies MySQL that the statements after Start should be cosidered as a single unit.
- `COMMIT` - used to save the data permanently
- `ROLLBACK` - used to get the data or restore the data to the last savepoint or last committed state
- `SAVEPOINT` - used to save the data at a particular point temporarily

##### Example

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

##### Transaction Properties (`ACID`)

- `Atomicity` - is combining all statements into a single unit. A transaction is considered to be atomic if it cannot be further broken down into individual operations and, all of the operations that occur within a transaction either succeed or fail as a single unit. If a single operation fails during a transaction, then everything is considered to have failed and must be rolled back.

- `Consistency` : One of the advantages of using a transaction is that, even if the transaction is a success or a failure, the database is consistent and the data integrity is maintained.
  All inconsistent data is removed, and all transactions that might cause inconsistency are aborted and an error is created or transcribed into an error log. Example: Consider two bank accounts ACC1 and ACC2 with funds of 10000$ and 9000, which is is total of 19000, after a transaction of transferring 50$ from ACC2 to ACC1 the funds in ACC1 is 10050$ and ACC2 are 8950$, which means the totals funds in AC1 and ACC2 adds up to 19000, So the funds in ACC1 and ACC2 are consistent before and after the Transaction.
- `Isolation`: Every transaction is isolated from other transactions. Therefore, a transaction shouldn't affect other transactions running at the same time. Stated another way, data modifications made by one transaction should be isolated from the data modifications made by other transactions. So, while a transaction can see data in the state it was in before another concurrent transaction modified it, as well as after the second transaction has completed, it cannot see any intermediate states. Example: Consider that the user A withdraws $100 and user B withdraws $250 from user ACC1 account, which has a balance of $1,000. Since both A and B draw from ACC1 account, one of the users is required to wait until the other user transaction is completed, avoiding inconsistent data.

- `Durability`:
  Transactions help with Durability in a few ways: data modifications that take place within a successful transaction may be safely considered to be stored in the database regardless of whatever else may occur. As each transaction is completed, a row is entered in the database transaction log. Thus, in the event of a system failure that requires the database to be restored from a backup you can use this transaction log to get the database back to the state it was in after a successful transaction.
  The ACID property of DBMS plays a vital role in maintaining the consistency and availability of data in the database

#### `DQL` Data Query Language. Search, filter, group, aggregate stored data

- `SELECT`

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

### Normalization

> What is normalization?

`Normalization` is the process of organizing the data and the attributes of a database.

- reduce the duplication of data, - avoid data anomalies
- ensure referential integrity
- simplify data management

1. `1NF` First Normal Form

- Each table cell should contain a single value.
- Each record needs to be unique
- violation example: hobbies with several values
- solution add new rows with each value

2. `2NF` Second Normal Form

- Be in 1NF
- Single Column Primary Key - that does not functionally dependant on any subset of candidate key relation
- violation example: name and address identifies a record when two different people have the same name
- solution: add a primary key column

3. `3NF` Third Normal Form

- in 2NF
- all the attributes (e.g. database columns) are functionally dependent on solely the primary key (no transitive functional dependencies)
- violation example: hospital database having a table of patients which included a column for the telephone number of their doctor. The phone number is dependent on the doctor, rather than the patient, thus would be better stored in a table of doctors
- solution: create table for doctors and store phone number there

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

### Constraints

> What are constraints and can you describe a few constraints?

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

### Basic Queries

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

### DML

The `DML` (`Data Management Language`) sublanguage of SQL is utilized to cre`ate, update, and delete data in a database.

- `INSERT`
- `UPDATE`
- `DELETE`

```sql
INSERT INTO roles (id, name) values (1, 'ADMIN'), (2, 'OWNER'), (3, 'EDITOR'), (4, 'VIEWER');

UPDATE permissions set categoryId=1;

DELETE FROM roles where name='VIEWER';
```

### DQL

- `Data Query Language`
- `SELECT` query

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

> Why would I use the WHERE clause?

- FILTERING: The filtering clause of a select statement is a `WHERE` clauses that defines how selected rows are filtered from the table. WHERE` clauses use **logical operators** to select records that meet specific conditions.
  - `AND` true if both boolean expresions evaluate to true
  - `IN` true if the operand is included in a list of expressions
  - `NOT` Reverses the value of any boolean expression
  - `OR` true if either or both boolean expressions is true
  - `LIKE` true if the operand matches a pattern
    - `%`` (percent) match any string of zero or more characters
    - `_` (underscore) match any single character
  - `BETWEEN` true if the operand falls within a range
    Where Logical operators
- `GROUP BY` groups rows that have the same values into summary rows. Often used with aggregate functions like `COUNT`, `MAX`, `MIN`.
- `HAVING` is used to filter out groups that meet a condition.
- `ORDER BY` clause is used to sort the returned records by a specified column. The records can be ordered either `ASC` (ascending) or `DESC` (descending). Ascending order is default if not specified.
- `LIMIT` clause restricts number of records returned from the select statement.
- `OFFSET` clause specifies from which record position to start counting from. This is often used in conjunction with the `LIMIT` clause. NOTE: Some SQL implementations use the `SKIP` keyword instead of offset

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

### Joins

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

### Set Operations

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

### Aggregate Functions
