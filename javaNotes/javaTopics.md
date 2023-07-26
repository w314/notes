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

### Result Set

- `java.sql.ResultSet` interface represents the result set of a query on a database
- The `ResultSet` is an object which represents a set of data returned from a database as a result of a query input.
- `executeQuery` method can be used to obtain the result table from the `SELECT` statement in a ResultSet object.

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

### Intro to JDBC API

_Note: You will not be assessed over the Implementation section of this activity_

`JDBC` stands for `Java Database Connectivity`. It is a relatively low-level API used to write Java code that interacts with relational databases via SQL.

In order to interact with a database, we need to do several things:

- Register the JDBC driver
- Open a connection using:
  - Database URL
  - Username
  - Password
- Execute some SQL statement using either:
- Statement
- PreparedStatement
- CallableStatement
- Retrieve the results that are returned in a `ResultSet` object

### DAO Design Pattern

The `DAO` (`Data Access Objects`) design pattern logically separates the code that accesses the database into Data Access Objects.

- To use the DAO design pattern, define an interface which declares methods through which the database will be queried.
- Then, concrete implementation classes can implement the interface and contain the data access logic to return the required data.

### Example

If we have an Employee table in our database we'd like to query, we would create a EmployeeDAO interface:

```java
public interface EmployeeDAO {
  // define some CRUD (Create, Read, Update, Delete) operations here
  public List<Employee> getAllEmployees();
  public List<Employee> getEmployeesByLocation(String location);
  public void updateEmployeeById(int id);
  public void deleteEmployeeById(int id);
  public void addEmployee(Employee e);
}
```

This interface would be implemented for a specific database - e.g. Oracle:

```java
public class EmployeeDAOImplOracle implements EmployeeDAO {
  public List<Employee> getAllEmployees() {
    List<Employee> list = new ArrayList<>();
    // JDBC code here...
	return list;
  };
  public List<Employee> getEmployeesByLocation(String location) {
    List<Employee> list = new ArrayList<>();
    // JDBC code here...
	return list;
  };
  public void updateEmployeeById(int id) {
    // JDBC code here...
  };
  public void deleteEmployeeById(int id) {
    // JDBC code here...
  };
  public void addEmployee(Employee e) {
    // JDBC code here...
  };
}
```

Now whenever we need to query the Employee table in the database, we have a simple, clean interface which abstracts the data access logic:

```java
EmployeeDAO dao = new EmployeeDAOImplOracle();
List<Employee> allEmpls = dao.getAllEmployees();
allEmpls.forEach( e -> System.out.println(e));

List<Employee> NYEmpls = dao.getEmployeesByLocation("New York");
NYEmpls.forEach( e -> System.out.println(e));
```

### Using ResultSet

_Note: You will not be assessed over Callable Statements / Stored Procedures this week
Note: You will not be assessed over the Persisting Data with JDBC topic_
