java, javalin, backend, dao, jdbc

## Maven

> What is Maven? Why would we use it?

`Maven` is a tool that can be used for building and managing any Java-based project.

We use it as Maven helps in:

- Simplifying the build process
- Adding jars and dependencies
- Documenting project information with change logs and reports
- Integration with source control systems (Git)

Maven project configuration and dependencies are handled via the `Project Object Model`, defined in the `pom.xml` file. This file contains information about the project, is used to build the project, includes project dependencies and plugins.

Some important tags within the pom.xml file include:

- `<project>` - this is the root tag of the file
- `<modelVersion>` - defining which version of the page object model to be used
- `<name>` - name of the project
- `<properties>` - project-specific settings
- `<dependencies>` - this is where you put your Java dependencies you want to use. Each one needs a `<dependency>`, which has:
  - `<groupId>`
  - `<artifactId>`
  - `<version>`
- `<plugins>` - for 3rd party plugins that work with Maven

## Java Backend Model

- Models - representing database tables
- DAO - interacting with the database
- Services - executing logic, validation
- Controller - server with endpoints

## DAO Layer

> What is the DAO Design Pattern and why should we use it?

### DAO Design Pattern

The `DAO` (`Data Access Objects`) design pattern logically separates the code that accesses the database into Data Access Objects.

- To use the DAO design pattern, define an interface which declares methods through which the database will be queried.

```java
public interface AccountDAO {

    // methods for CRUD Operations

    // CREATE
    public Account createAccount(Account account);

    // READ
    // UPDATE
    // DELETE
}
```

- Then, concrete implementation classes can implement the interface and contain the data access logic to return the required data.

```java
public class AccountDAOmySQLImpl implements AccountDAO {
  @Override
  public Account createAccount(Account account) {
    // connect to db
    // create account
    // return account created
  }
}
```

Now whenever we need to query the database, we have a simple, clean interface which abstracts the data access logic.

> What is the JDBC API and the benefits of using it?

### `Java Database Connectivity` (`JDBC`)

- low-level API
- interacts with relational databases via SQL
- database agnostic
- uses database drivers which implement the interfaces defined in the JDBC API for the given database

#### How to use the `JDBC` to interact with the datase

In order to interact with a database, we need to do several things:

1. register the JDBC driver
2. open a database connection
3. execute the SQL statements using
4. process the ResultSet

#### 1. Register the `JDBC` driver

To register the JDBC driver for a specific database, add it as a `dependency` in the `pom.xml` file (except oracle)

```xml
  <dependencies>
    <!-- https://mvnrepository.com/artifact/com.mysql/mysql-connector-j -->
    <dependency>
      <groupId>com.mysql</groupId>
      <artifactId>mysql-connector-j</artifactId>
      <version>8.1.0</version>
    </dependency>
</dependencies>
```

#### 2. Open a database connection

> What information would you need in order to successfully connect to a database?

- database URL (`JDBC String`)
- username
- password

```java
// try-with-resources syntax automatically closes the database
try (
  Connetion conn = DriverManager.getConnection(DB_URL,USERNAME,PASSWORD)) {
  // more code goes here
} catch (SQLException e) {}
```

- use the `DriverManager` class to get a Connection
- need URL, username, and password.
- these parameters should be stored in an external configuration file
- a `Connection` object is returned
- close your resources: the `try-with-resources syntax` is used to automatically close the connection being created after the block ends

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

Once we have the `Connection object`, we can write our SQL and execute it.

- use connection object to execute sql statements
- results that are returned in a `ResultSet` object
- types of sql statements:
  - Statement
  - PreparedStatement
  - CallableStatement

##### `Statement`

The `Statement interface` is used for executing static SQL statements.

```java
Statement stmt = conn.createStatement();
String sql = "SELECT * FROM employees";
ResultSet rs = stmt.executeQuery(sql);
```

##### `Prepared Statment`

> What is the difference between a Simple and Prepared JDBC statement?

> What is SQL Injection and how can we prevent it using the JDBC?

`SQL Injections` are the exploitation of programming weaknesses in SQL codes to gain access to a database, its resources, and applications.

`PreparedStatement` can be used to prevent SQL injections.

- specifies parameters with the ? symbol
- protects against SQL injection when user input is used by pre-compiling the SQL statement

The `PreparedStatement interface` is used for executing pre-compiled SQL statements.

- Protects against SQL injection

- This interface gives us the flexibility of specifying parameters with the `?`symbol.

- Protects against `SQL injection` when user input is used by pre-compiling the SQL statement

> What is SQL Injection and how can we prevent it using the JDBC?

`SQL Injections` are the exploitation of programming weaknesses in SQL codes to gain access to a database, its resources, and applications.

`PreparedStatement` can be used to prevent SQL injections.

- specify parameters with the ? symbol
- protects against SQL injection when user input is used by pre-compiling th

##### `.executeQuery`

- returns a ResultSet object

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

##### `.executeUpdate()`

- for DML statements, returns an int which is the number of rows affected

In case of inserting a record where the primary key is autogenerated:

```java
// create sql string
String sql = "INSERT INTO account (username, password) VALUES (?, ?);";

// create  a preparedStatement
// use Statement interface's RETURN_GENERATED_KEYS field
// to make sure the generated account_id is returned
PreparedStatement ps = conn.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS);
// set the parameters
ps.setString(1, username);
ps.setString(2, password);

// execute preparedStatement
ps.executeUpdate();

// process result
ResultSet keys = ps.getGeneratedKeys();
while(keys.next()){
    // get returned account_id
    int account_id = keys.getInt("account_id");
    // return new account
    return new Account(account_id, username, password);
            }
```

The Statement and PreparedStatement also have additional methods for sending SQL, including:

- `.execute()` - for any kind of SQL statement, returns a boolean

- This interface gives us the flexibility of specifying parameters with the `?`symbol.

- Protects against `SQL injection` when user input is used by pre-compiling the SQL statement

#### Additional methods to send `SQL`

The `Statement` and `PreparedStatement` also have additional methods for sending SQL, including:

- `.execute()` - for any kind of SQL statement, returns a `boolean`

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

<hr>
# JUST COPIED
<hr>

### Using ResultSet

_Note: You will not be assessed over Callable Statements / Stored Procedures this week
Note: You will not be assessed over the Persisting Data with JDBC topic_

### Result Set

- `java.sql.ResultSet` interface represents the result set of a query on a database
- The `ResultSet` is an object which represents a set of data returned from a database as a result of a query input.
- `executeQuery` method can be used to obtain the result table from the `SELECT` statement in a ResultSet object.

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

- This interface gives us the flexibility of specifying parameters with the `?`symbol.

- Protects against `SQL injection` when user input is used by pre-compiling the SQL statement

#### Additional methods to send `SQL`

The `Statement` and `PreparedStatement` also have additional methods for sending SQL, including:

- `.execute()` - for any kind of SQL statement, returns a `boolean`
- `.executeUpdate()` - for `DML` statements, returns an `int` which is the number of rows affected

## Service Layer

## Controller

### Javalin

> Describe Javalin.

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
- Javalin runs on an embedded Jetty.
- Javalin can be used to start and stop the server.
- do not need to have any custom configuration, you can just quick-start a server in Javalin
- configuration is done through the `Javalin.create()` method
- You can customize the embedded server in Javalin
- You can configure your embedded jetty-server and Javalin will attach it’s own handlers to the end of the chain.

#### How to use Javalin

1. install Javalin as a dependency
2. create a Javalin object
3. create endpoints
4. create handlers

#### Add Javalin as a dependency

To use Javalin add it as a dependency to `POM.xml`:

```xml
 <!-- https://mvnrepository.com/artifact/io.javalin/javalin -->
  <dependency>
    <groupId>io.javalin</groupId>
    <artifactId>javalin</artifactId>
    <version>5.5.0</version>
  </dependency>
```

### Create a Controller with Javalin

```java
// import for Javalin
import io.javalin.Javalin;
import io.javalin.http.Context;
// import Service class
import Service.AccountService

// controller class
public class AccountController {

  // declare our service variable
  AccountService accountService;

  // constructor
  public SocialMediaController() {
      accountService = new AccountService();
  }

  // this method can be called by our main app
  // return a Javalin object
  public Javalin startAPI() {
      // create javalin app
      Javalin app = Javalin.create();

      // create endpoints with path and handler
      app.post("/register", this::createUser);

      // return javalin app
      return app;
  }

  // handler method
    private void createUser(Context ctx) {
      // get information from request ctx object
      Account account = ctx.bodyAsClass(Account.class);

      // call account service to validate input and create account
      Account accountCreated = accountService.createAccount(account);

      // send response based on the result of the service call
      // if account was succesfully created
      if( accountCreated != null) {
          // set status to 200
          ctx.status(200);
          // send account added as json in response body
          ctx.json(accountCreated);
      // if there was en error to create the account
    } else {
        // set status to 400
        ctx.status(400);
    }

}
```

### Javalin Handlers

> What is a handler?

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

##### `endpoint-handlers`

- the main handler type, and defines your API.
- GET handler to server data to a client, or a POST handler to receive some data. Common methods are supported directly on the Javalin class (GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS), uncommon operations (TRACE, CONNECT) are supported via Javalin#addHandler

- endpoint-handlers are matched in the order they are defined.

##### handlers with path parameters

- Handler paths can include path-parameters.
- These are available via `ctx.pathParam("key")`

```java
// the {} syntax does not allow slashes ('/') as part of the parameter
app.get("/hello/{name}", ctx -> {
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

###### set response

- the Handler interface has a void return type. - use methods of the context object to set the response
  - ctx.result(result)
  - ctx.json(obj) - sends object as JSON
  - ctx.future(future)

##### `before-handlers`

```java
app.before(ctx -> {
  // runs before all requests
});
app.before("/path/*", ctx -> {
  // runs before request to /path/*
});
```

##### `after-handlers`

Run after every request (even if an exception occurred). You might know after-handlers as filters, interceptors, or middleware from other libraries.

```java
app.after(ctx -> {
    // run after all requests
});
app.after("/path/*", ctx -> {
    // runs after request to /path/*
});
```

You need to be familiar with basic request/response methods that you can use with the context object like:

- result()
- json()
- status()
- body()

_You do not need to know all the methods of the context object_

_You do not need to know about Future objects_

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
