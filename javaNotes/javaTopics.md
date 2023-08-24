## SQL

> What is SQL and why would we use this language

`Structured Query Language` (`SQL`) is the language used to administer SQL-based RDBM systems.

### Database

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

#### `DCL` Data Control Language - manage access permissions to database object

- `GRANT`
- `REVOKE`

#### `TCL` Transaction Control Language. Defines concurrent operation boundaries

- `COMMIT`
- `ROLLBACK`
- `SAVEPOINT`

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

## Operating System

> What is an operating system?

- a software that communicates with the hardware and allows other programs to run
- it is comprised of system software, or the fundamental files your computer needs to boot up and function
- they allow you to install and run programs written for the operating system
- every device (computer, tablet, phone) has an operating system
- the hardware you choose affects what operating system(s) you can run (Windows on PC hardware, Mac OS X Apple, Linux on both)

Functions Operating Systems Provide

- Process and `Process Management` (`process` is a program in execution)
- `Threads` - a thread as a flow of execution through the process code. The thread keeps track of all the instructions that need to be executed next in the program counter. Also, the thread contains system registers that hold the current working variables. Also, the thread's stack contains the execution history.

- `Scheduling` - in scheduling, the process manager takes the responsibility to remove the running process from the CPU and chooses another process based on a specific strategy.
- `Memory Management` - the functionality of an operating system that handles and manages the primary memory. Processes move back and forth between the main memory and the disk during the execution.

## Java Programming Language

> Java What are some of the benefits of Java?

- platform independent,
- has a C-language inspired syntax
- provides automatic memory management
- has an extensive built-in runtime library
- is supported by the Oracle corporation
- has a rich open source community

## Java Compilation Process

> What is the difference between source code and bytecode?

- Compilation means to transform a program written in a high-level programming language from `source code` into `object code` / `bytecode`.
- `.java` -> `.class`

> How would you describe the compilation process for Java?

2 steps compilation process:

- compiler creates machine independent `bytecode`
- `JVM` creates machine code

> What is the difference between the JDK, JRE, and JVM?

`JDK` `Java Development Kit` contains `JRE` and development tools like compiler, debugger, documentation tools.

`JRE` (`Java Runtime Environment`) contains `JVM` and runtime libraries.

`JVM` (`Java Virtual Machine`) runs compiled bytecode in a virtual environment that is same accross every platform. However you need JVM that is specific to the operating system. It uses `JIT` `Just In Time` compiler to turn that bytecode to machine code.

## Java Entities

> Can you describe some of the basic entities of a Java program?

- classes
- variables
- methods

`Classes` are blueprints for creating objects in Java. Classes can have variables and methods within them to represent state and behavior.

`Variables` are containers to store data.

`Methods` are blocks of reusable code.

## Java Variables

> What is a variable?

A `variable` is a container for storing data.

```java
dataType variableName = value;
```

Java is strongly typed meaning that when a variable is declared in Java, the type must be specified.

Variable Types:

- primitive type - data types defined by the language itself
- reference type - data types defined in the Java API or by a programmer

The `variable name` is the unique identifier used to reference that variable again.

> What is the difference between assigning and declaring a variable?

DECLARE a variable

```java
datatype variableName;
```

- Java is a strongly-typed language which means that all variables in Java must define what type of data we can store into that variable.
- This statement creates a place in memory for Java to store information of that specific datatype.
- camelCase naming convention
- We can refer to this named place in memory using the variable name. If we want to store a value in the variable

ASSIGN a value to a variable

```java
variableName = value;
```

- stores a value in the variable
- only work as long as the new variable is of the same datatype

> What is a primitive data type? Please list a few and explain them.

- data types defined by the language
- stores the value of the data
- types
  - boolean 1 bit true or false
  - byte 1 byte numerical
  - char 2 bytes 1 character
  - short 2 bytes numerical
  - int 4 bytes numerical
  - float 4 bytes floating point
  - long 8 bytes numerical
  - double 8 bytes floating point

## Java Methods

> What is a method?

A `method` is a block of reusable code that can be invoked again and again.

> What is the difference in syntax between calling a method and creating a method?

`Method Signature`

All methods in a class are defined by:

- their access modifier
- any non-access modifiers
- return type
- method name
- (optionally) a throws exception declaration

Together, these form the `method signature`.

`Method Parameters`

- Method parameters are variables passed inside of the parenthesis of the method which we are able to utilize inside of our method. These values are given to us from the entity that invokes the method.

```java
// METHOD CREATION SYNTAX
int addNums(int n1, int n2) {
  return n1 + n2;
}

// METHOD CALL SYNTAX
addNums(1, 2);
// storing method return value
// method return value's type = variable type
int total = addNums(1, 2);

```

> Explain the main method.

```java
public class HelloWorld{
  public static void main(String[] args) {
    System.out.println("Hello, World!");
  }
}
```

- `public` is an access modifier
- `static` is a non-access modifier
- `void` is the "return type" of the method
- `String[] args` array of Strings defined in the method parameters are passed from the command line when the java command is run

## Java Conditional Statements

Conditional statements are flow control statments.

> What is a conditional statement?

`Conditional statement` is a statement that uses a Boolean expressions and only executes the a block of statement if the Boolean expression returns `true`.

- `if` - execute a statement or a block of statements only if some conditional test turns out to be true
- `switch` - execute one of several blocks of statements depending on the value of a variable of certain types
- while
- do-while

> When would you use an if statement over a switch statement?

- `switch` statement works with:
  - `byte`, `short`, `int`
  - `char`, `String`
  - `enum`
- if the if statement is too long switch can be better

## Java Loops

Loops are flow control statments.

> Explain the different kinds of loops you can create and use in a program.

`Loops` are java statements that allow for the repeated execution of the same statement or block of statements.

```java
// FOR loop
for (int i = 1; i < 10; i++) {
  System.out.println(i);
}

// ENHANCED FOR loop
// for iterables
int[] arr = [1, 2, 3];
for(int n: arr) {
  System.out.println(n);
}


// WHILE loop
int i = 0;
while (i < 3) {
  System.out.println(i);
  i++;
}

// DO WHILE loop
int i = 4;
do {
  System.out.println(i);
} while(i < 3);

```

## print statements

## Scanner class

> What is the Scanner class used for? Give an example of how you would use it.

The `Scanner` class is used to get user input.

- found in the `java.util` package

```java
import java.util.Scanner;

class Main {
  public static void main(String[] args) {
    // create Scanner object
    Scanner myScanner = new Scanner();
    // prompt user for input
    System.out.println("Enter username:");
    // read and store user input
    String userName = myScanner.nextLine();
    myScanner.close();
  }
}
```

Methods:

- `nextBoolean()` Reads a boolean value from the user
- `nextByte()` Reads a byte value from the user
- `nextDouble()` Reads a double value from the user
- `nextFloat()` Reads a float value from the user
- `nextInt()` Reads a int value from the user
- `nextLine()` Reads a String value from the user
- `nextLong()` Reads a long value from the user
- `nextShort()` Reads a short value from the user

If you enter wrong input (e.g. text in a numerical input), you will get an exception/error message (like `InputMismatchException`).

## String class

> Which datatype represents text in Java?

Strings.

- are not a primitive data type but a reference type
- a string variable holds a reference to an object created from the String class, not the value of the string itself
- Strings are immutable, constant objectsm, this is accomplished by having internal, private and final fields and not implementing any "setter" methods which would alter the state of those fields.
- Because Strings are immutable, all of the methods in the String class return a new String - the original is not modified.
- When Strings are created they are placed in a special location within the `heap` called the `String Pool`.
- When String literals are created, if there is an existing String that matches in the String Pool, the reference variable will point to the existing value.
- Duplicates will not exist in the String Pool. This is important because Strings take up a lot of memory. Being able to reuse the same value throughout your application is advantageous.
- One way to circumvent the above process is to use the new keyword along with the String constructor, which will explicitly create a new String object in memory, even if one already exists in the String Pool.

The String API consists of the following:

- `toUpperCase()` -Converts all the characters of a string to upper case.
- `toLowerCase()`-Converts all the characters of a string to lower case
- `charAt(int index)` -This returns the indexed character of a string, where the index of the initial character is 0
- `concat(String s)` -This returns a new string consisting which has the old string + s
- `equals(String s)` -Checks if two strings are equal
- `equaIsIgnoreCase(String s)` -This is like equals(), but it ignores the case(Ex: ‘Hello’ and ‘hello’ are equal)
- `length( )` -Returns the number of characters in the current string.
- `replace(char old, char new)` -This returns a new string, generated by replacing every occurrence of old with new.
- `trim()` -Returns the string that results from removing white space characters from the beginning and ending of the current string.

### Using Operators

_Note: You will not be assessed on bitwise or shift operators_

### Basic Debugging

### Reading a Stacktrace

## Java Arrays

> What is an array? Why is it useful?

An `array` is a `contiguous block of memory` storing a group of `sequentially stored` elements of the same type. Provies fast data access.

- fixed size and cannot be resized after declaration
- items in an array are referenced via their index in square bracket notation, which begins with 0 for the first element
- ave a length property specifying the length of the array

```java
int[] myArray = new int[5];
// OR
int[] otherArray = {1, 2, 3};
```

> How can you iterate over an array?

> How would you access the last value in an array if you do not know the size of the array?

## Using Database in Java

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

`HTTP` (`HyperText Transfer Protocol`) is a technique of transmitting data in a particular format, primarily between a server and a

HTTP works by a client making a connection to a `server`, sending a `request`, and receiving a `response`

The data tranmitted can be:

- `hypertext` - A text documents that have the special ability to link to one another.
- `hypermedia` - hypertext documents that have the ability to show multiple kinds of media

A request contains:

- the `method` being used
- the `URL` where the target is
- version of HTTP is being used
- Optional information to help the server with the request (called `headers`)
- For some methods, a `body` which contains some resources (ex.: files to be uploaded)

A response contains:

- version of HTTP is being used
- status code reflecting the outcome of the request
- status message which is shorthand and less descriptive than the status code
- Optional information to detail what happened with the request (called `headers` again)
- For some methods, a body which contains some resource (ex. file to be downloaded)

### HTTP verbs

_You should be familiar with GET, POST, PUT, and DELETE_

- GET
  - used to retrieve data from a server at the specified resource
  - does not modifying any resources
  - safe and `idempotent` method
- POST
  - used to send data to the API server to create or update a resource
  - the data sent to the server is stored in the request body of the HTTP request
  - `non-idempotent`
- PUT
  - similar to POST, PUT requests are used to send data to the API to update or create a resource
  - `idempotent`, calling the same PUT request multiple times will always produce the same result
  - when a PUT request creates a resource the server will respond with a 201 (Created), and if the request modifies existing resource the server will return a 200 (OK) or 204 (No Content)
- HEAD
- DELETE

  - deletes the resource at the specified URL

- PATCH
- OPTIONS

### HTTP status codes

_You need to know what each category of status represents as well as common status codes (200, 201, 400, 404, 500)_

HTTP Status Codes whether a specific HTTP request has been successfully completed.

Responses are grouped in five classes:

- Informational responses (100–199)
- Successful responses (200–299)
- Redirection messages (300–399)
- Client error responses (400–499)
- Server error responses (500–599)

Common Status Codes:

- 200 - OK, success
- 201 - Created
- 400 - Bad Request, client error
- 404 - Not Found
- 500 - Internal Server Error

Week 6 Assessment

## functional programming in Java

- `functional programming` uses functions to solve problems
- specifying what you want to happen to get results, not how you want it to happen
- (use predefined functions and rely heavily on chaining function calls, not on creating structure, like classes where we define the "how")

---

# Key Concept

- wherever we have a functional interface reference variable / parameter, we have a position where we can use a lambda (or method reference)
- functional interfaces enable functional programming in Java

### functional interfaces

- interfaces that have only one abstract method
- are used with `lambda` expression (the parameter types and return types of the lambda must match the functional interface method declaration)
- a way of introducing functional programming to Java
- The [Java 8 JDK comes with many built-in functional interfaces](https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html): `forEach()` method of the `Iterable interface`
- We can also use functional interfaces as types to which we can assign lambda functions, like so:

```java
// declare functional interface
interface MyFunctionalInt {
  int doMath(int number);
}

public class Execute {
  public static void main(String[] args) {
    // use functional interface as types and assign lambda function to them
    MyFunctionalInt doubleIt = n -> n * 2;
    MyFunctionalInt subtractIt = n -> n - 2;

    int result1 = doubleIt.doMath(2); // result1 = 4
    int result2 = subtractIt.doMath(8); // result2 = 6
    }
}
```

### lambdas

- short lived, in-line implementation of a `functional interface`
- a lot of the syntax for creating a lambda can be omitted for conciseness
- inside the `lambda` expression `this` refers to the enclosing class of the lambda expression
- they introduce some important aspects of `functional programming` to Java

Syntax:

```java
() -> 42;
(int x, int y) -> x + y;
(int x, int y) -> {
  System.out.prinln("printing something");
  return x + y;
}
myArray.forEach(n -> System.out.println(n));
```

### method references

- lambda with even shorter syntax
- can be used if all you need to perform is a method call quickly
- 4 types:
  - static methods
  - instance method of a particular object
  - instance method of a particular type
  - constructor

Syntax

```java
// 1. Static methods
// ContainingClass::staticMethodName
List<String> messages = Arrays.asList("hello", "revature" "associates!");
// simple lambda expression
messages.forEach(word -> StringUtils.capitalize(word));
// method reference syntax
messages.forEach(StringUtils::capitalize);

// 2. instance methods of particular objects
// ContainingObject::instanceMethodName

// 3. Instance methods of an arbitrary object of a particular type
// syntax: `ContainingType::methodName`
// example: `String::toString`

// 4. Constructor
// syntax: `ClassName::new`
```

## Javalin

- lightweight web framework forJava 8+ and `Kotlin`
- a web framework's role is to make web development easier
- not opinionated: you can structure your project how you want
- provides a Context object for working with requests and responses
- It supports modern features such as:
  - HTTP/2
  - WebSocket
  - asynchronous requests.
- `servlet-based`
- has first-class interoperability between Java and `Kotlin`
- never extends classes and rarely implements interfaces

### How to use Javalin

1. install Javalin as a dependency
2. create a Javalin object
3. create endpoints

#### Install Javalin as a dependency

To use Javalin add it as a dependency to `POM.xml`:

```xml
 <!-- https://mvnrepository.com/artifact/io.javalin/javalin -->
  <dependency>
    <groupId>io.javalin</groupId>
    <artifactId>javalin</artifactId>
    <version>5.5.0</version>
  </dependency>
```

#### Create Javalin App

Javalin "Hello World":

```java
import io.javalin.Javalin;

public static void main(String[] args) {
  // create a Javalin object
  Javalin app = Javalin.create().start(7000);
  // create endpoint
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
- do not need to have any custom configuration, you can just quick-start a server in Javalin
- configuration is done through the `Javalin.create()` method
- You can customize the embedded server in Javalin
- You can configure your embedded jetty-server and Javalin will attach it’s own handlers to the end of the chain.

### Handlers

- respond to client requests
- Javalin has three main handler types:
  - before-handlers
  - endpoint-handlers
  - after-handlers
- The before-, endpoint- and after-handlers require three parts:
  - `verb`, one of: before, get, post, put, patch, delete, after (… head, options, trace, connect)
  - `path`, ex: /, /hello-world, /hello/{name}
  - handler implementation, ex ctx -> { ... }
- The Handler interface has a void return type. You use a method like ctx.result(result), ctx.json(obj), or ctx.future(future) to set the response which will be returned to the user.

#### Main Javalin Handler Types:

1.  `before-handlers`

```java
app.before(ctx -> {
  // runs before all requests
});
app.before("/path/*", ctx -> {
  // runs before request to /path/*
});
```

2. `after-handlers`

Run after every request (even if an exception occurred). You might know after-handlers as filters, interceptors, or middleware from other libraries.

```java
app.after(ctx -> {
    // run after all requests
});
app.after("/path/*", ctx -> {
    // runs after request to /path/*
});
```

3.  `endpoint-handlers`

- the main handler type, and defines your API. You can add a GET handler to server data to a client, or a POST handler to receive some data. Common methods are supported directly on the Javalin class (GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS), uncommon operations (TRACE, CONNECT) are supported via Javalin#addHandler

- endpoint-handlers are matched in the order they are defined.

- Handler paths can include path-parameters. These are available via ctx.pathParam("key"):

```java
app.get("/hello/{name}", ctx -> { // the {} syntax does not allow slashes ('/') as part of the parameter
    ctx.result("Hello: " + ctx.pathParam("name"));
});
```

- handler paths can also include wildcard parameters:

```java
app.get("/path/*", ctx -> { // will match anything starting with /path/
    ctx.result("You are here because " + ctx.path() + " matches " + ctx.matchedPath());
});
```

However, you cannot extract the value of a wildcard. Use a slash accepting path-parameter (`<param-name>`) if you need this behavior.

The Handler interface has a void return type. You use a method like ctx.result(result), ctx.json(obj), or ctx.future(future) to set the response which will be returned to the user.

### Javalin Context Object

- contains request and response information and functionality
- getting info from request: `pathParam()` or `bodyAsClass()`
- sending info to the client: `result()` or `json()`

#### Request methods

Getting information from requests

```java
body() // request body as string
```

If we include `Jackson` as a dependency, we can parse JSON request bodies automatically into our model classes. For instance:

```java
app.post("/") { ctx ->
  User user = ctx.bodyAsClass(User.class);
}
```

#### Response methods

- `result("result")` - set result stream to specified string (overwrites any previously set result)
- `result(byteArray)` - set result stream to specified byte array (overwrites any previously set result)
- `result(inputStream)` - set result stream to specified input stream (overwrites any previously set result)
- `status(code)` - set the response status code
- `status()` - get the response status code
- `json(obj)` - calls result(jsonString), and also sets content type to json

## JSON

_ignore implementation, the second part of it is in JavaScript_

- `JSON` (`JavaScript Object Notation`) is a lightweight data-interchange format.
- JSON Object is a set of key and value pair enclosed within curly braces
- a key is a string enclosed in quotation marks
- a value can be a:
  - string
  - number
  - boolean expression
  - array, or object
- `parse()` is a commonly used method or function name used to read JSON strings in a variety of programming
  languages.

JSON object syntax:

```javascript
let Book = {
  id: 110,
  language: "Python",
  author: ["John", "Ben"],
};
```

Applications of JSON:

- transmit data between the server and web application
- helps transmit and serialize all types of structured data
- allows us to perform asynchronous data calls without the need to do a page refresh
- Web services and Restful APIs use the JSON format to get public data.

## REST

_You will not be assessed over the example in the Implementation section (we will not cover Servlets)_

DEFINITION:

> Representational State Transfer (REST) is an architectural style that defines a set of constraints to be used for creating web services.

- Representational State Transfer
- architecture for exposing information and functionality between software or devices
- used to fetch or give some information from a web service
- information provided is a representation of the state of a given resource
- representation is usually JSON
- all communication done via REST API uses only HTTP requests
- In HTTP there are five methods that are commonly used in a REST-based Architecture: POST, GET, PUT, PATCH, and DELETE. These correspond to create, read, update, and delete (or CRUD) operations respectively.

`REST` vs.<br>
`SOAP` (`Simple Access Protocol`) and <br>
`RPC` (`Remote Procedure Call`)

- REST uses less bandwidth than SOAP
- SOAP can only return `xml`, REST can return json, xml, yaml and more
- in REST users are not required to know procedure names or spedific parameters in a specific order like in RPC

### Is RESTful API right for the application

There are some key `constraints` to think about when considering whether a RESTful API is the right type of API for your needs:

- `Client-Server`: This constraint operates on the concept that the client and the server should be separate from each other and allowed to evolve individually.
- `Stateless`: REST APIs are stateless, meaning that calls can be made independently of one another, and each call contains all of the data necessary to complete itself successfully.
- `Cache`: Because a stateless API can increase request overhead by handling large loads of incoming and outbound calls, a REST API should be designed to encourage the storage of cacheable data.
- `Uniform Interface`: The key to the decoupling client from server is having a uniform interface that allows independent evolution of the application without having the application’s services, or models and actions, tightly coupled to the API layer itself.
- `Layered System`: REST APIs have different layers of their architecture working together to build a hierarchy that helps create a more scalable and modular application.
- `Code on Demand`: Code on Demand allows for code or applets to be transmitted via the API for use within the application.

### REST resources and url construction

#### REST Resource

- entity or data that API can provide info about
- can be identified by a URL
- can allow actions to be performed on it (GET, POST, PUT, DELETE)

Singleton and Collection Resources
A resource can be a singleton or a collection.

For example, “customers” is a collection resource and “customer” is a singleton resource (in a banking domain).

We can identify “customers” collection resource using the URI “/customers“. We can identify a single “customer” resource using the URI “/customers/{customerId}“.

Collection and Sub-collection Resources
A resource may contain sub-collection resources also.

For example, sub-collection resource “accounts” of a particular “customer” can be identified using the URN “/customers/{customerId}/accounts” (in a banking domain).

Similarly, a singleton resource “account” inside the sub-collection resource “accounts” can be identified as follows: “/customers/{customerId}/accounts/{accountId}“.

### URI

`REST API`s use Uniform Resource Identifiers (`URI`s) to address resources.

The constraint of a uniform interface is partially addressed by the combination of URIs and HTTP verbs and using them in line with the standards and conventions.

# Constraints (principles)

- client/server relationship: separate components interacting through an interface
- uniform interface: use of resources, self-descriptive messages
- stateless: each message contains all info needed
- HATEOS / Hypertext as the engine of application state (make API discoverable in state through links!)
- layered system: application itself is ideally in layers interacting through interfaces
- cachable: responses should specify if info is cachable or not.

### Best Practices

- use nouns for resources (users, posts, etc) not verbs
- use plurals for resources that are collections
- single resources are represented by a name or id
- send appropriate response code back

resource archetypes categories:

- document
- collection
- store
- controller

Put a resource into one archetype and then use its naming convention consistently.

For uniformity’s sake, resist the temptation to design resources that are hybrids of more than one archetype.

#### document

A document resource is a singular concept that is akin to an object instance or database record.

In REST, you can view it as a single resource inside resource collection. A document’s state representation typically includes both fields with values and links to other related resources.

Use “singular” name to denote document resource archetype.

http://api.example.com/device-management/managed-devices/{device-id}
http://api.example.com/user-management/users/{id}
http://api.example.com/user-management/users/admin

#### collection

A collection resource is a server-managed directory of resources.

Clients may propose new resources to be added to a collection. However, it is up to the collection resource to choose to create a new resource or not.

A collection resource chooses what it wants to contain and also decides the URIs of each contained resource.

Use the “plural” name to denote the collection resource archetype.

http://api.example.com/device-management/managed-devices
http://api.example.com/user-management/users
http://api.example.com/user-management/users/{id}/accounts

#### store

A store is a client-managed resource repository. A store resource lets an API client put resources in, get them back out, and decide when to delete them.

A store never generates new URIs. Instead, each stored resource has a URI. The URI was chosen by a client when the resource initially put it into the store.

Use “plural” name to denote store resource archetype.

http://api.example.com/song-management/users/{id}/playlists

#### controller

A controller resource models a procedural concept. Controller resources are like executable functions, with parameters and return values, inputs, and outputs.

Use “verb” to denote controller archetype.

http://api.example.com/cart-management/users/{id}/cart/checkout http://api.example.com/song-management/users/{id}/playlist/play

Consistency is the key
Use consistent resource naming conventions and URI formatting for minimum ambiguity and maximum readability and maintainability. You may implement the below design hints to achieve consistency:

- Use forward slash (/) to indicate hierarchical relationships
  The forward-slash (/) character is used in the path portion of the URI to indicate a hierarchical relationship between resources. e.g.

http://api.example.com/device-management
http://api.example.com/device-management/managed-devices
http://api.example.com/device-management/managed-devices/{id}
http://api.example.com/device-management/managed-devices/{id}/scripts
http://api.example.com/device-management/managed-devices/{id}/scripts/{id}

- Do not use trailing forward slash (/) in URIs
  As the last character within a URI’s path, a forward slash (/) adds no semantic value and may confuse. It’s better to drop it from the URI.

http://api.example.com/device-management/managed-devices/ http://api.example.com/device-management/managed-devices /_This is much better version_/

- Use hyphens (-) to improve the readability of URIs
  To make your URIs easy for people to scan and interpret, use the hyphen (-) character to improve the readability of names in long path segments.

http://api.example.com/device-management/managed-devices/
http://api.example.com/device-management/managed-devices /_This is much better version_/
Do not use underscores ( _ )
It’s possible to use an underscore in place of a hyphen to be used as a separator – But depending on the application’s font, it is possible that the underscore (_) character can either get partially obscured or completely hidden in some browsers or screens.

To avoid this confusion, use hyphens (-) instead of underscores ( \_ ).

http://api.example.com/inventory-management/managed-entities/{id}/install-script-location //More readable

http://api.example.com/inventory-management/managedEntities/{id}/installScriptLocation //Less readable

- Use lowercase letters in URIs

- do not use file extensions

Apart from the above reason, if you want to highlight the media type of API using file extension, then you should rely on the media type, as communicated through the Content-Type header, to determine how to process the body’s content.

http://api.example.com/device-management/managed-devices.xml /_Do not use it_/

http://api.example.com/device-management/managed-devices /_This is correct URI_/

- Use query component to filter URI collection
  Often, you will encounter requirements where you will need a collection of resources sorted, filtered, or limited based on some specific resource attribute.

For this requirement, do not create new APIs – instead, enable sorting, filtering, and pagination capabilities in resource collection API and pass the input parameters as query parameters. e.g.

http://api.example.com/device-management/managed-devices
http://api.example.com/device-management/managed-devices?region=USA
http://api.example.com/device-management/managed-devices?region=USA&brand=XYZ
http://api.example.com/device-management/managed-devices?region=USA&brand=XYZ&sort=installation-date

### Exposing and Consuming RESTful API endpoints

_You will not be assessed over implementation code of steps 3 and 4 (Bennu Framework)_

## Logging

> What is logging and what are the benefits of it?
>
> Logging is keeping a log of events that occur form an application.

### Logback

- `Logback` is one of the most widely used logging frameworks in the Java Community.(It's a replacement for its predecessor, Log4j.)
- Logback offers:
  - faster implementation
  - more options for configuration
  - more flexibility in archiving old log files
  - smaller memory footprint

Resons to prefer `Logback` over `Log4j`:

- small and speedy: components are faster and have a smaller memroy footprint
- much better tested framework
- automatically reloads configuration files
- gracefully recovers from I/O errors (no need to restart app after server fail, just to get logging to work again)
- automatic removel of old log archives
- automatic compression of archived log files

### Logback Architecture

The `Logback architecture` is comprised of three classes:

- `Logger` - object that allows you to create logs
- `Appender` - represents the destination of a log
- `Layout` - controls log message formatting

### How to use a Logger

> How would we configure logging in an application?

1. configure logger
2. use logger objects in classes you want to use logging
3. use the logger object's logging level method

### Logging Levels

> Describe the different logging levels and how they should be used.

- TRACE - most fine-grained information
- DEBUG - should be used for information that may be needed for diagnosing issues and troubleshooting
- INFO - standard log level
- WARN - indicates that something unexpected happened, but the code can continue the work
- ERROR - hould be used when the application hits an issue preventing one or more functionalities from properly functioning

Setting level at a certain level gives all level on and above that level.

What are logging levels good for?

- filtering
- allow you to configure your logging process so that it behaves differently according to each level:
  - Granularity. It might make sense to decrease or increase the granularity of logging according to the level.
  - Target. You might want level X entries to be logged to files, and level Y entries to be logged to a database.
  - Retention policy. This is linked to granularity. If a certain level has a higher granularity, it might make sense to delete the log entries in that level more frequently, for example, to save disk space.

#### Setup & Configuration

- if no configuration is given, default logger can be used
- default logger uses debug logging level
- to configure create `logback.xml` file under `main/resources`
- create appenders
- create loggers and assign them appenders

##### Add dependency to `pom.xml`

`Logback` uses the Simple Logging Facade for Java (`SLF4J`).

`Classpath`
Logback also requires logback-classic.jar on the classpath for runtime.

We'll add this to `pom.xml` as a test dependency:

```xml
<!-- https://mvnrepository.com/artifact/ch.qos.logback/logback-classic -->
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.4.11</version>
    <scope>test</scope>
</dependency>
```

##### Add `logback.xml` configuration file

We'll create a text file named `logback.xml` and put it somewhere in our classpath:

```xml
<configuration>
  <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
    <encoder>
      <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
    </encoder>
  </appender>

  <root level="debug">
    <appender-ref ref="STDOUT" />
  </root>
</configuration>
```

#### Use Logger

```java
package main;

public class Example {

    // create logger object
    private static final Logger logger = LoggerFactory.getLogger(Example.class);

    // use logging methods
    public static void main(String[] args) {
        logger.info("Example log from {}", Example.class.getSimpleName());
    }
}
```

## Mockito

> What is Mockito and why would we use it?

> What is a mock?

### Mockito

Mocking framework used for unit tests

A mock object is a dummy implementation for an interface or a class.

Mockito records the interaction with mock and allows you to check if the mock object was used correct, e.g. if a certain method has been called on the mock. This allows you to implement behavior testing instead of only testing the result of method calls.

Mockito:

- uses annotations to identify its functionality, similar to JUnit
- `mock`: replacement object - behavior is stubbed unless we request real behavior
- `spy`: replacement object - behavior is real unless we request it is stubbed
- from the docs: "Real spies should be used carefully and occasionally, for example when dealing with legacy code."
- `stub`: replacement behavior

### Creating Mocks

Dependency Injection using @Mock, @InjectMock, and @openMocks

_NOTE: @openMocks is the syntax used in newer versions of Mockito and it replaces @initMocks. Both do the same thing._

- `@InjectMocks` is used on the object being tested to specify what to inject with a mock
- `@Mock` to specify what should be mocked
- `MockitoAnnotations.openMocks()` is used to perform the injection
- Mockito will use any constructors available in the real object for injection, otherwise it will try using setters, and then finally it will try using fields

### Stubbing

- when() is used to target an invocation
- thenReturn() or thenThrow() is used to return dummy results / throw exceptions
- if a mock's method isn't stubbed, it will return default values (null, empty collection, 0, false, etc)
- doThrow(), doAnswer(), doNothing(), doCallRealMethod() are used with void methods (https://www.baeldung.com/mockito-void-methods)

### Verify

- a mock will remember all method invocations on it for verification
- `times(x)` is used to verify a behavior was invoked x many times
- `never()` is used to verify a behavior was not invoked
- `atMostOnce()`, `atLeastOnce()`, `atMost(x)`, `atLeast(x)`

WK7

## Generics

- enables classes to be parameterized so they can be re-used with different types as input, like methods
- alternative is using Object as type of state, which would require casting and could lead to runtime issues
- generics add stability to your code by making more of your bugs detectable at compile time

### creating a class that uses generics

- add a generic type declaration to your class, ex `ClassName<T>`
- you can specify more than one type variable as a parameter
- use the type variables throughout the class
- `bounded types`: requirement that type must be subtype or of same type as specified type
  - ex: `ClassName<T extends SuperType>`
  - supertype can be a class or interface

### using a generic class

- generic type invocation: when using the parameterized class, replace the type param name with the actual type you want to use
- ex: `ArrayList<String> stringList`
- raw type: if you do not specify a type, the Object type will be used

### type parameter naming conventions

Type params are single, uppercase letters.

- E: Element
- K: Key
- N: Number
- T: Generic Data Type
- V: Value
- S,U,V etc: 2nd, 3rd, 4th for multiple generic data types

## Iterators

- objects that allow you to traverse a Collection
- are used "behind the scenes" in enhanced for loops

The `Iterable` interface defines a data structure which can be directly traversed using the `.iterator()` method, which returns an `Iterator`.

- Any class that implements the Iterable interface needs to override the `iterator()` method
- Any class implementing the Iterator interface needs to override the `hasNext()` and `next()` methods provided by the Iterator interface.
- The Iterator instance stores the iteration state. That means it provides utility methods to get the current element, check if the next element exists, and move forward to the next element if present. In other words, an Iterator remembers the current position in a collection and returns the next item in sequence if present. The Iterable, on the other hand, doesn’t maintain any such iteration state
- The contract for Iterable is that it should produce a new instance of an Iterator every time the iterator() method is called. This is because the Iterator instance maintains the iteration state, and things won’t work as if the implementation returns the same Iterator twice.
- For an Iterable, we can move forward only in the forward direction, but some of the Iterator subinterface like ListIterator allows us to move back and forth over a List.
- Also, Iterable doesn’t provide any method to modify its elements, nor can we modify them using the for-each loop. But Iterator allows removing elements from the underlying collection during the iteration with the remove() method.

### Iterator Methods:

- `.hasNext()` - returns true if the iteration has more elements
- `.next()` - returns the next element in the iteration.
- `.remove()` - removes element from underlying collection (can only be called on modifiable Collections!)
- you cannot modify using Collection methods during iteration!

### List Iterator

- additionally has operations that use indexes
- can iterate backwards
- `.nextIndex()`
- `.previousIndex()`
- `.previous()`
- `.hasPrevious()`

### `Iterable`

An Iterable represents a collection that can be traversed.

To traverse an iterable:

#### 1. `Enhanced For Loop`

```java
Set<String> names = new ArrayList<>();

for (String name : names) {
  System.out.println(name);
}
```

### 2. using an `Iterator`

```java
Iterator<Integer> iterator = Arrays.asList(1, 2, 3, 4, 5).iterator();
while (iterator.hasNext()) {
    System.out.println(iterator.next());
}
```

### 3. using `.forEach()`

```java
Iterator<Integer> iterator = Arrays.asList(1, 2, 3, 4, 5).iterator();
iterator.forEachRemaining(System.out::println);
```

### 4. using `lambda`

```java
for (Integer i: (Iterable<Integer>) () -> iterator) {
    System.out.println(i);
}
```

## Collection API

_Assessment: Not PriorityQueue or Vector. Know how to work with Collections and yes, knowing the difference between a linked list and arraylist is useful._

> What is a Collection?

A `collection` is a single object which acts as a container for other objects.

> What is the Collection API?
> Java has the Collection API that implements common data structures

### Important Interfaces

- `Iterable`: requires that subtypes must be iterable so it can be traversed using a for-each loop
- `Collection`: defines common behavior that all subtypes should have (add, remove, contains, etc)
- `Set`: defines set-specific behaviors
- `List`: defines list-specific behaviors
- `Queue`: defines queue-specific behaviors
- `Deque`: extends `Queue` supports double-ended queue
- `Map`: does not implement the Collection or Iterable interfaces, but is part of the collection framework.

## Queue

- FIFO: add to end/tail, remove from beginning/head
- Java has an interface that represents this data structure
- operations unique to queues:
  - `offer`: attempt and adds, if you are able to
  - `peek`: attempt to get head, if there is one
  - `poll`: attempt and remove, if you are able to
- using add(), remove(), and element() would throw exceptions

### Queue implementations

- `LinkedList`
- `ArrayDeque`
  - resizable array implementation of `Deque`interface
- `PriorityQueue`
  - elements are ordered by priority based on their natural ordering (or a Comparator)
- `ArrayBlockingQueue`
  - array-backed
  - implements `BlockingQueue` interface
  - supports operations that wait on the queue to contain an element or for space to become available in the queue
  - Solution to the producer-consumer problem, where a producer thread inputs elements into the array while a consumer thread removes them for processing

## Stack

- LIFO: add to end/top, remove from end/top
- Java has a legacy class that represents this data structure
- Java recommends the Deque type instead
- stack operations:
  - `push`: add to top
  - `peek`: view top
  - `pop`: remove top

## Sets

- collection that does not contain duplicates
- this interface provides set operations (union, intersection, difference)

### Implementations

- HashSet: insertion order not guaranteed
- LinkedHashSet: maintains insertion order
- TreeSet: elements are sorted

### Useful Methods

- addAll() - (union) adds elements from one set to the other, no duplicates
- retainAll() - (intersection) retains only common elements between two sets
- removeAll() - (difference) removes all elements from first set that are contained in second set

## Maps

- each entry in a map is a key-value pair
- specifies two generic type parameters
- keys are unique
- part of the `Collections Framework`
- does NOT implement `Collections interface`
- there are 2 interfaces for implementing `Map` in Java:
  - `Map`
  - `SortedMap`

### Implementations

- `HashMap`
  - does NOT maintain order of insertion
  - fast insertion/retreival
  - permits 1 null key and null values
  - `HashTable`:
    - older, thread safe implementation of `HashMap`
    - does not allow null keys or null values
- `LinkedHashMap`
  - maintains insertion order
- `TreeMap`
  - entries are sorted by keys
  - keys are stored in a Sorted Tree structure
  - slow insertion/retreival
  - cannot contain null keys

### Useful Methods

- put()
- get()
- remove()
- entrySet()
- keySet()
- values()

### Iterating over map

- does NOT implement the `Iterable interface`
- therefore cannot be iterated over directly
- use instead
  - `.entrySet()` method to iterate over `Map.Entry`
  - `.keySet()` method to iterate over keys
  - `.values()` method return a `Collection` that can be iterated over

## ArrayList Class

- implements the `List` interface
- a data structure which contains an array within it, but can resize dynamically.
- Once it reaches maximum capacity, an ArrayList will increase its size by 50% by copying its elements to a new (internal) array.
- Traversal is fast (constant time) because elements can be randomly accessed via index, just like an array.
- Insertion or removal of elements is slow, however (linear time, since there is a risk of having to resize the underlying array)
- ArrayList is a parameterized type
- cannot use primitives, must use their wrapper classes
- better for storing and accessing data

## LinkedList Class

- implements both the `List` and `Dequeue` interfaces
- the data structure is composed of nodes internally, each with a reference to the previous node and the next node - i.e. a doubly-linked list.
- insertion or removal of elements is fast
- traversal is slow for an arbitrary index
- better for manipulating data (vs. storing and accessing)

### Linked List Methods

- addFirst()
- addLast()
- getFirst()
- getLast()
- indexOf()
- get() (uses index)
- listIterator()

## ArrayList vs. LinkedList

- When the rate of addition or removal rate is more than the read scenarios, then use a LinkedList. On the other hand, when the frequency of the read scenarios is more than the addition or removal rate, then ArrayList takes precedence over LinkedList.
- Since the elements of an ArrayList are stored more compact as compared to a LinkedList; therefore, the ArrayList is more cache-friendly as compared to the LinkedList. Thus, chances for the cache miss are less in an ArrayList as compared to a LinkedList. Generally, it is considered that a LinkedList is poor in cache-locality.
- Memory overhead in the LinkedList is more as compared to the ArrayList. It is because, in a LinkedList, we have two extra links (next and previous) as it is required to store the address of the previous and the next nodes, and these links consume extra space. Such links are not present in an ArrayList.
- ArrayList in the multithreading environment does not provide thread safety. This is because ArrayList is not synchronized.

## common UNIX commands

> What are some common Linux commands? Why are they useful?

```shell
#  list directory content
ls

# change directory
cd

# display current working directory path
pwd

# create directory
mkdir

# create empty file
touch

# echo redirected to file with > will create new file
echo "New file content" > new_file.txt

# view file
cat filename

# create new file
cat > newfile

# copy sourcefile content to destionation file
cat sourcefile > destinationfile

# search string in file
grep mystring myfile

# compare 2 files, output lines that are different
diff file1 file2

# move file1 to directory1
mv file1 directory1
# prompt if we would overwrite a file
mv - i file1 directory1
# do not move if we would overwrite a file
mv -n file1 directory1
# only move if the source file is newer than destination file
mv -u file1 directory1
# create backup of overwritten destination file with same name 1 added to end
mv -b file1 directory1

# rename file1 to file2
mv file1 file2

# copy file1 to file2
cp file1 file2
# flags
# interactive, warn before overwriting
-i
# create backup of destination file
-b
# use force: delete destination file if cannot be opened
-f
# recursive, copy directory with all subdirectories
-r
# preserve characteristics: times of last modification, etc
-p

# delete file
rm file1
# delete directory with all files and subdirectories
rm -r directory1
# force deletion flag
-f



mv
rm

cat
grep
cp
```

## source control management

> What is source control management? Why is it useful?

`Version control` = Revision control = `Source Control Management` (`SCM`), is a process to manage a collection of source code and its changes.

- manage and keep track of all your source code
- all your changes are being stored in a repository.
- there are 2 types of Version Control Systems
  - the Centralized Version Control System (CVCS)
  - Distributed (DVCS).

The concept of `CVCS` is that it works on a Client-Server relationship. The repository is located in one place and provides access to many clients.

On the contrary, in `DVCS`, every user has a local copy of the repository in addition to the central repo on the server-side.

## Git

- you have the entire history of the project right there on your local disk

> What are the main states that your files can reside in when using Git?

Git has three main `states` that your files can reside in:

- `modified` - you have changed the file but have not committed it to your database yet
- `staged` - you have marked a modified file in its current version to go into your next commit snapshot.
- `committed` - the data is safely stored in your local database

> What are the main sections of a Git project?

The three main `sections` of a Git project:

- the `working tree` (or `working directory`, as in the diagram below) is a single checkout of one version of the project, downloaded to your local machine. The working tree is the set of all files and folders a developer can add, edit, rename and delete during application development. These files are pulled out of the compressed database in the Git directory and placed on disk for you to use or modify.
- the `staging area` is a file, generally contained in your Git directory, that stores information about what will go into your next commit. Its technical name in Git parlance is the `“index”`, but the phrase “staging area” works just as well. (See diagram below)
- `Git directory`(a.k.a. `repository folder`) is where Git stores the metadata and object database for your project. This is the most important part of Git, and it is what is copied when you clone a repository from another computer
  - stores the history of all changes made to the files in a Git project
  - name of directory: `.git`

Two types of Git repositories, based on user permissions:

- Bare Repositories
  - Software development teams use bare repositories to share changes made by team members.
  - Individual users aren't allowed to modify or create new versions of the repository.
- Non-Bare Repositories

  - With non-bare repositories, users can modify the existing repository and create new versions.
  - By default, the cloning process creates a non-bare repository.

  > What are some common operations you would be performing when using Git?

- Understand how to push to repo
- Understand how to use branches
- Understand how to merge

```shell
# initialize repository
git init

# clone repository
git clone [url] [directory]

# get status of git repository
git status

# stage all files in directory
git add .

# commit changes
git commit -m 'commit message'

# push code to remote repository
git push

# create new branch
git branch new-branch

# move to new branch
git checkout new-branch

# shortcut to create and move to new branch
get checkout -b new-branch

# pull data from remote repository
git pull

# merge branch to master
#  1. move to master first
git checkout master
#  2. merge new branch
git merge new-branch
```

### Git Bash

- Git Bash is an application for Microsoft Windows environments which provides an emulation layer for a Git command line experience. A package that installs Bash, some common bash utilities, and Git on a Windows operating system.
- `Bash` is an acronym for `Bourne Again Shell`
- `shell` is a terminal application used to interface with an operating system through written commands.
- `Bash` is a popular default shell on Linux and macOS.

wk8

Week 8 Assessment

## MORE SQL

### DCL

### TCL

### Transactions

Transaction properties

### aggregate functions

### scalar functions

### GROUP BY

### Functions

### Stored Procedures

### Triggers

### Sequences

### Indexes

## Algorithm

_Note: The types of algorithms mentioned in the lesson are supplementary to know._

## The common Big O Notations

Factory Pattern
Singleton Pattern
Day 4
_NOTE: You will not be assessed over the algorithm implementation details. Understand them at a high level._
Bubble Sort
Merge Sort
Binary Search
Linear Search
