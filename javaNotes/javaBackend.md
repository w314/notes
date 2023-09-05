java, javalin, backend, dao, jdbc

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

### 70 What are the Maven build lifecycle phases?

When Maven builds your project, it goes through several steps called phases

- `validate`: validate the project is correct and all necessary information is available
- `compile`: compile the source code of the project
- `test`: test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
- `package`: take the compiled code and package it in its distributable format, such as a JAR.
- `verify` - run any checks on results of integration tests to ensure quality criteria are met
- `install` - install the package into the local repository, for use as a dependency in other projects locally
- `deploy` - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.

### 71 Describe the POM.xml file and its importance.

`POM` - `Project Object Model`

In `Maven` the project coordinates below together uniquely identify a specific version of a program:

- `group-id`: company name for example: "com.revature"
- `artifact-id`: project name
- `version`: version number for example: "0.0.1-SNAPSHOT"

#### Some other important tags within the `pom.xml` file include:

`<project>` - this is the root tag of the file

- `<modelVersion>` - defining which version of the page object model to be used
- `<properties>` - project-specific settings
- `<dependencies>`: this is where you put your Java dependencies you want to use. Each one needs a
  - `<dependency>` which has:
    - `<groupId>`
    - `<artifactId>`
    - `<version>`
- `<plugins>` for 3rd party plugins that work with Maven

Here's an example:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project>
    <modelVersion>4.0.0</modelVersion>
    <!-- project metadata-->
    <groupId>org.revature</groupId>
    <artifactId>PEPLabsChallenges</artifactId>
    <version>0.1</version>

    <!-- maven allows us to change the version of java we'd like to use -->
    <properties>
        <maven.compiler.source>11</maven.compiler.source>
        <maven.compiler.target>11</maven.compiler.target>
    </properties>

    <!--
        maven allows us to use external dependencies from mvn repository.
    -->
    <dependencies>
        <!-- junit, our framework for writing unit tests.-->
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.13.2</version>
        </dependency>
    </dependencies>
</project>
```

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

## Testing

### 67 What is test driven development?

The `TDD` process consists of writing unit tests first, **before** the implemented application code has been written.

`Unit testing` is the testing of individual software components in isolation from the rest of the system.

### 68 Why are unit tests important?

`Unit testing` is the testing of individual software components in isolation from the rest of the system. This is done by writing unit tests which execute the code we want to inspect.

When developing software, it is important to ensure that most if not all of the code being written is tested to verify the functionality of the code.

One way to ensure this is to follow a process called test-driven development, or TDD.
The TDD process consists of writing unit tests first, before the implemented application code has been written. Then, the implemented application code can be written to make the test pass and the process can be completed for each piece of functionality required.

When refactoring code, the unit tests give us confidence that we can change the source code without breaking existing functionality. This makes debugging much easier.

### 69 How can JUnit annotations help with running our tests?

To use Junit add it as a dependency to `pom.xml`

```xml
			<dependency>
				<groupId>org.junit.jupiter</groupId>
				<artifactId>junit-jupiter-api</artifactId>
				<version>5.10.0-M1</version>
				<scope>test</scope>
			</dependency>

```

`Annotations` are used to support, identify, and execute test method features.

- `@BeforeAll`
- `@BeforeEach`
- `@AfterEach`
- `@AfterAll`
- `@Test`

### Mockito

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
