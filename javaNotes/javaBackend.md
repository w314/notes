## GET DATA FROM DATABASE

### JDBC

> What is the JDBC API and the benefits of using it?

`Java Database Connectivity` (`JDBC`)

- low-level API
- interacts with relational databases via SQL
- database agnostic
- uses database drivers which implement the interfaces defined in the JDBC API for the given database

How to use the `JDBC`

1. register connection - as a `dependency` except for Oracle
2. open connection - need url, username & password
3. execute sql statements - statement, preparedStatement,

#### 1. Open a connection

```java
// try-with-resources syntax
try (
  Connection conn = DriverManager.getConnection(DB_URL,USERNAME,PASSWORD)) {
  // more code goes here
} catch (SQLException e) {}
```

- use the DriverManager class to get a Connection
- need URL, username, and password.
- these parameters should be stored in an external configuration file
- close your resources
- try-with-resources syntax is used to automatically close the Connection being created after the block ends

`JDBC String`

- the database `URL`
- the address pointing to the database to be used
- the format of this URL varies between database vendors, in `MySQL`
  - JDBC Driver: `com.mysql.jdbc.Driver`
  - URL format: `jdbc:mysql://hostname/databaseName`

`Autocommit mode`

- default
- every SQL statement acts as a transaction and is committed immediately after execution
- to manually group statements into a transaction, simply call:

```java
Connection conn = DriverManager.getConnection(DB_URL,USERNAME,PASSWORD);
conn.setAutoCommit(false);

// execute some SQL statements...
conn.commit();
```

#### 2. Execute SQL statements

- use connection object to execute sql statements
- results that are returned in a `ResultSet` object

### Statement vs Prepared Statement

> What is the difference between a Simple and Prepared JDBC statement?

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
// set sql string
String sql = "SELECT * FROM employees WHERE age > ? AND location = ?";

// create preparedStatement
PreparedStatement ps = conn.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS);
ps.setInt(1, 40);
ps.setString(2, "New York");

// execute preparedStatement
ResultSet rs = ps.executeQuery(sql);
```

- pre-compiled SQL statement
- protects against SQL injection

The Statement and PreparedStatement also have additional methods for sending SQL, including:

- `.execute()` - for any kind of SQL statement, returns a boolean
- `.executeUpdate()` - for DML statements, returns an int which is the number of rows affected

- This interface gives us the flexibility of specifying parameters with the `?`symbol.

- Protects against `SQL injection` when user input is used by pre-compiling the SQL statement

> What is SQL Injection and how can we prevent it using the JDBC?

`SQL Injections` are the exploitation of programming weaknesses in SQL codes to gain access to a database, its resources, and applications.

`PreparedStatement` can be used to prevent SQL injections.

- specify parameters with the ? symbol
- protects against SQL injection when user input is used by pre-compiling the SQL statement

#### Additional methods to send `SQL`

The `Statement` and `PreparedStatement` also have additional methods for sending SQL, including:

- `.execute()` - for any kind of SQL statement, returns a `boolean`
- `.executeUpdate()` - for `DML` statements, returns an `int` which is the number of rows affected

#### 3. Use ResultSet

`ResultSet`is an object which represents a set of data returned from a database as a result of a query input. Can be iterated over.

```java
List<Employee> empList = new ArrayList<>();
while (rs.next()) {
  int id = rs.getInt("id");
  String name = rs.getString("first_name");
  empList.add(new Employee(id, name));
}
```

> What is the DAO Design Pattern and why should we use it?

The `DAO` (`Data Access Objects`) design pattern logically separates the code that accesses the database into Data Access Objects.

1. DAO interface with methods to query the database
2. db specific implementation classes implement our interface query the database and return the required data

EXAMPLE

1. DAO interface

```java
public interface EmployeeDAO {
  // define some CRUD (Create, Read, Update, Delete) operations here
  public List<Employee> getAllEmployees();
  public void addEmployee(Employee e);
}
```

2. Oracle specific class implements DAO interface

```java
public class EmployeeDAOImplOracle implements EmployeeDAO {
  public List<Employee> getAllEmployees() {
    List<Employee> list = new ArrayList<>();

    // JDBC code here
    Statement stmt = conn.createStatement();
    String sql = "SELECT * FROM employees";
    ResultSet rs = stmt.executeQuery(sql);
    while (rs.next()) {
      int id = rs.getInt("id");
      String name = rs.getString("first_name");
      list.add(new Employee(id, name));

    return list;
  };
  public void addEmployee(Employee e) {
    // JDBC code here...
  };
}
```

3. Query DB through DAO

```java
EmployeeDAO dao = new EmployeeDAOImplOracle();

List<Employee> allEmpls = dao.getAllEmployees();
allEmpls.forEach( e -> System.out.println(e));
```

_Note: You will not be assessed over Callable Statements / Stored Procedures this week
Note: You will not be assessed over the Persisting Data with JDBC topic_

> What information would you need in order to successfully connect to a database?

- URL (`JDBC String`)
- username
- password

```java
// try-with-resources syntax
try (
  Connection conn = DriverManager.getConnection(DB_URL,USERNAME,PASSWORD)) {
  // more code goes here
} catch (SQLException e) {}
```

- use the DriverManager class to get a Connection
- need URL, username, and password.
- these parameters should be stored in an external configuration file
- close your resources
- try-with-resources syntax is used to automatically close the Connection being created after the block ends

`JDBC String`

- the database `URL`
- the address pointing to the database to be used
- the format of this URL varies between database vendors, in `MySQL`
  - JDBC Driver: `com.mysql.jdbc.Driver`
  - URL format: `jdbc:mysql://hostname/databaseName`

`Autocommit mode`

- default
- every SQL statement acts as a transaction and is committed immediately after execution
- to manually group statements into a transaction, simply call:

```java
Connection conn = DriverManager.getConnection(DB_URL,USERNAME,PASSWORD);
conn.setAutoCommit(false);

// execute some SQL statements...
conn.commit();
```
