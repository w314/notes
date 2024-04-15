java, javalin, backend, dao, jdbc

## Common UNIX Commands

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
```

- > see git

## Maven

> What is Maven? Why would we use it?

`Maven` is a tool that can be used for building and managing any Java-based project.

We use it as Maven helps in:

- Simplifying the build process
- Adding jars and dependencies
- Documenting project information with change logs and reports
- Integration with source control systems (Git)

Maven project configuration and dependencies are handled via the `Project Object Model`, defined in the `pom.xml` file. This file contains information about the project, is used to build the project, includes project dependencies and plugins.

### Maven build lifecycle phases

> What are the Maven build lifecycle phases?

When Maven builds your project, it goes through several steps called phases

- `validate`: validate the project is correct and all necessary information is available
- `compile`: compile the source code of the project
- `test`: test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
- `package`: take the compiled code and package it in its distributable format, such as a JAR.
- `verify` - run any checks on results of integration tests to ensure quality criteria are met
- `install` - install the package into the local repository, for use as a dependency in other projects locally
- `deploy` - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.

### `POM` - `Project Object Model`

> Describe the POM.xml file and its importance.

`pom.xml` declares metadata about the project, including project coordinates, dependencies, and plugins.

In `Maven` the project coordinates below together uniquely identify a specific version of a program:

- `group-id`: company name for example: "com.revature"
- `artifact-id`: project name
- `version`: version number for example: "0.0.1-SNAPSHOT"

POM.xml example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!-- root tag of the file -->
<project>
    <!-- version of the page object model to be used -->
    <modelVersion>4.0.0</modelVersion>
    <!-- project metadata, that identifies the project-->
    <groupId>org.revature</groupId>
    <artifactId>PEPLabsChallenges</artifactId>
    <version>0.1</version>

    <!-- version of java we'd like to use -->
    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
    </properties>

    <!-- external dependencies from mvn repository. -->
    <dependencies>

        <!-- junit, our framework for writing unit tests.-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
        </dependency>

    </dependencies>

    <!-- for 3rd party plugins that work with Maven -->
    <plugins>
    </plugins>

</project>
```

## JSON

Data interchange format.

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

```json
let Book = {
  "id": 110,
  "language": "Python",
  "author": ["John", "Ben"],
};
```

Applications of JSON:

- transmit data between the server and web application
- helps transmit and serialize all types of structured data
- allows us to perform asynchronous data calls without the need to do a page refresh
- Web services and Restful APIs use the JSON format to get public data.

-> see rest

## Logging

> What is logging and what are the benefits of it?

> Logging is keeping a log of events that occur form an application.

### Logback

- `Logback` is one of the most widely used logging frameworks in the Java Community.(It's a replacement for its predecessor, Log4j.)
- Logback offers:
  - faster implementation
  - more options for configuration
  - more flexibility in archiving old log files
  - smaller memory footprint

Resons to prefer `Logback` over `Log4j`:

- small and speedy: components are faster and have a smaller memory footprint
- much better tested framework
- automatically reloads configuration files
- gracefully recovers from I/O errors (no need to restart app after server fail, just to get logging to work again)
- automatic removal of old log archives
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

#### Logging Levels Are Used For

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
 - > see testing
 
## Fullstack Applications

### What is and application

- software: bundles of files
- performs a task
- 3 main parts

#### 1. Front-End

- user interface
- command-line interface OR
- graphical user interface

#### 2. Back-End

- logic
- responding to front-end code
- interacting with database

#### 3. Database

- data storage

## Java Backend

### N-Tier Architecture

- separates app into layers that are each responsible for a group of related tasks
- layers interact with one another through interfaces you define
- benefits: more organized, flexible, and maintainable code

#### Layers

- Controller
  - takes input from client
  - calls service layer for decision making
  - sends output afterward
- Service
  - takes input from controller
  - makes decisions (validation, error handling)
  - communicates with DAO layer if data management needed
  - returns information to controller
- DAO
  - takes input from service layer
  - performs CRUD operations on database
  - returns a result to service layer
- Models
  - contains classes that represent entities (like DB tables)

### DAO Layer

- `Data Access Object`
- object responsible for CRUD operations on an entity

> What is the DAO Design Pattern and why should we use it?

#### DAO Design Pattern

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

#### `Java Database Connectivity` (`JDBC`)

- Java API that allows us to interact with a database
- found within the `java.sql` package
- database agnostic
- for connection requires
  - database driver
  - db URL
  - db credentials
- database driver
  - other software that acts as mediator between Java and DB
  - implement the interfaces defined in the JDBC API for the given database

##### JDBC API Classes or Interfaces

- Connection
- DriverManager
- Statement
- PreparedStatement
- SQLException

##### How to use the `JDBC` to interact with the datase

0. register the JDBC driver
1. establish a connection
2. create a statement
3. execute the statement
4. process the results
5. close the connection

##### Register the `JDBC` driver

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

##### Open a database connection

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

##### Execute SQL statements

Once we have the `Connection object`, we can write our SQL and execute it.

- use connection object to execute sql statements
- results that are returned in a `ResultSet` object
- types of sql statements:
  - Statement
  - PreparedStatement
  - CallableStatement

##### `Statement`

The `Statement interface` TODO: INTERFACE? is used for executing static SQL statements.

```java
Statement stmt = conn.createStatement();
String sql = "SELECT * FROM employees";
ResultSet rs = stmt.executeQuery(sql);
```

###### `Prepared Statment`

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

###### SQL Injections

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

#### Use the ResultSet

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
- in a ResultSet column names are case insensitive

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
