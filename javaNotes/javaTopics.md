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

## Week 5 Assessment

### Statement vs Prepared Statement

Once we have the `Connection object`, we can write our SQL and execute it.

#### `Statement`

The `Statement interface` is used for executing static SQL statements.

```java
Statement stmt = conn.createStatement();
String sql = "SELECT * FROM employees";
ResultSet rs = stmt.executeQuery(sql);
```

#### `Prepared Statment`

The `PreparedStatement interface` is used for executing pre-compiled SQL statements.

```java
PreparedStatement ps = conn.prepareStatement();
String sql = "SELECT * FROM employees WHERE age > ? AND location = ?";
ps.setInt(1, 40);
ps.setString(2, "New York");
ResultSet rs = ps.executeQuery(sql);
```

- This interface gives us the flexibility of specifying parameters with the `?`symbol.

- Protects against `SQL injection` when user input is used by pre-compiling the SQL statement

#### Additional methods to send `SQL`

The `Statement` and `PreparedStatement` also have additional methods for sending SQL, including:

- `.execute()` - for any kind of SQL statement, returns a `boolean`
- `.executeUpdate()` - for `DML` statements, returns an `int` which is the number of rows affected

### SQL Injection

_You will need to know why Prepared Statements can help prevent SQL Injection. All other information in the Preventing SQL Injection activity is supplementary._

### Properties file

_You will NOT be assessed over the written material: Configuring a Connection Factory once Connection Pooling is introduced_

A `properties file` stores information as key value pairs, each on their own line; the file has a `.properties` extension.

- security
- one place to change values (in case of changing password)

```java
FileInputStream fileStream = new FileInputStream("pathtopropertiesfile");
Properties properties = new Properties();
properties.load(fileStream);
URL = properties.getProperty("URL");
CONNECTION_PASSWORD = properties.getProperty("CONNECTION_PASSWORD");
CONNECTION_USERNAME = properties.getProperty("CONNECTION_USERNAME");
```

### Foreign Key

### Normalization

_1NF, 2NF, and 3NF_

`Normalization` is the process of organizing the data and the attributes of a database. it is performed to reduce the data redundancy.

First, second, and third normal forms are stepping stones to the `Boyce-Codd normal form` and, when appropriate, the higher normal forms.

#### 1NF

A relation is in `1NF` (`First Normal Form`) if:

- all its attributes have an atomic value (each column must have only one value for each row in the table)
- there must be a primary key for identification
- no duplicated rows or columns

#### 2NF

A relation is in `2NF` if it is:

- in `1NF`
- all non-key attributes are completely dependent only on the `Primary Key`, no hidden dependencies

#### 3NF

A relation is in 3NF if:

- in 2NF
- there is no transitive dependency

The attributes should be mutually independent which means, none of the attributes should be functionally dependent on any combination of attributes. This mutual independence makes sure that any update on the individual attribute will not affect other attributes in a row.

### Referential Integrity

`REFERENTIAL INTEGRITY` is the relationship between tables.

Referential Integrity:

- requires that a foreign key cannot be defined unless its corresponding primary key exists is a referential integrity constrain.
- does not allow the addition of any record in a table that contains the foreign key unless the reference table contains a corresponding primary key.
- does not allow to deletion of a record in a table that contains the foreign key, to delete the record in the parent table, the corresponding record in the child table should be deleted first. to solve this issue `ON DELETE CASCADE` is used.
- Other options are to set the foreign key to null or to its default value (only if the default value references an existing value in the primary-key table).

### Composite Key

`Composite Key` is combining two or more keys in a table to create a primary key to uniquly identify a record.

It is also known as `Compound Key`, where each attribute creating a key is a `foreign key`.

### Join

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

### Set Operators

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

### View

Views, which are a type of virtual tables.

### HTTP Introduction

### HTTP verbs

_You should be familiar with GET, POST, PUT, and DELETE_

### HTTP status codes

_You need to know what each category of status represents as well as common status codes (200, 201, 400, 404, 500)_

Week 6 Assessment

### functional interfaces

- Functional interfaces are interfaces that have only one abstract method.
  This method is what lambdas are implementing when they are declared - the parameter types and return types of the lambda must match the functional interface method declaration.
- The Java 8 JDK comes with many built-in functional interfaces: `forEach()` method of the `Iterable interface`

```java
interface MyFunctionalInt {
  int doMath(int number);
}

public class Execute {
  public static void main(String[] args) {
    MyFunctionalInt doubleIt = n -> n * 2;
    MyFunctionalInt subtractIt = n -> n - 2;
    int result1 = doubleIt.doMath(2);
    int result2 = subtractIt.doMath(8);
    System.out.println(result1); // 4
    System.out.println(result2); // 6
    }
}
```

### lambdas

_Note: You will not be assessed over anonymous inner classes_

Are expressions with the syntax:

```java
parameter(s) -> expression
```

- are used to implement the abstract method of a `functional interface`
- they introduce some important aspects of `functional programming` to Java
- are one of the biggest new features of Java 8

### method references

_Note: You will not be assessed over “Instance methods of an arbitrary object of a particular type”
Note: You will not be assessed over the use of streams (The Stream API) this week_

Method references are a special type of lambda expressions.

There are four kinds of method references:

- Static methods

```java
ContainingClass::staticMethodName
```

```java
List<String> messages = Arrays.asList("hello", "revature" "associates!");
// simple lambda expression
messages.forEach(word -> StringUtils.capitalize(word));
// method reference syntax
messages.forEach(StringUtils::capitalize);
```

- Instance methods of particular objects

```java
ContainingObject::instanceMethodName
```

- Instance methods of an arbitrary object of a particular type

```java
ContainingType::methodName
String::toString
```

- Constructor

```java
ClassName::new
```

### Javalin

`Javalin` is a very lightweight `web framework` for Java 8 (and later) and Kotlin.

- It supports modern features such as HTTP/2, WebSocket, and asynchronous requests.
- Javalin is servlet-based, and its main goals are simplicity, a great developer experience, and first-class interoperability between Java and Kotlin.
- Javalin never extends classes and rarely implements interfaces

To use Javalin add it as a dependency to `POM.xml`:

```xml
<dependency>
    <groupid>io.javalin</groupid>
    <artifactid>javalin</artifactid>
    <version>2.5.0</version>
</dependency>
```

Javalin "Hello World":

```java
import io.javalin.Javalin;

public static void main(String[] args) {
    Javalin app = Javalin.create().start(7000);
    app.get("/", ctx -> ctx.result("Hello World"));
}
```

### Configuration

_You will not be assessed over custom configuration, customer server, or custom jetty handlers_

You need to be familiar with basic request/response methods that you can use with the context object like:

- result()
- json()
- status()
- body()

_You do not need to know all the methods of the context object_

_You do not need to know about Future objects_

- Javalin runs on an embedded Jetty.
- Javalin can be used to start and stop the server.
- If you don’t need any custom configuration, you can quick-start a server in Javalin
- You can customize the embedded server in Javalin
- You can configure your embedded jetty-server and Javalin will attach it’s own handlers to the end of the chain.

### JSON

_ignore implementation, the second part of it is in JavaScript_

### Introduction to REST

_You will not be assessed over the example in the Implementation section (we will not cover Servlets)_

### REST resources and url construction

### Exposing and Consuming RESTful API endpoints

_You will not be assessed over implementation code of steps 3 and 4 (Bennu Framework)_

### Mockito

#### Dependency Injection using @Mock, @InjectMock, and @openMocks

NOTE: @openMocks is the syntax used in newer versions of Mockito and it replaces @initMocks. Both do the same thing.

#### using when() and thenReturn()

#### know what a Spy is conceptually

#### using verify()

### Logback

#### Real World Application is supplementary

#### Architecture

#### Logging Levels

#### Basic Configuration

#### Creating and Using a Logger

WK7
