jdbc

# JDBC

> `Java Database Connectivity API` is a Java API used to connect to a database and run queries on them.
- part of standard edition of Java (JavaSE)
- requires a `JDBC Driver` for database connection


## Data Persistence
>`Data Persistence` means for an application to store and retrieve data from a non-volatile storage.
- `Data` - what to persist
- `Medium` - how to persist
- `Storage` - where to persist

> `Medium` is the thing that is used to transfer data from source to destination.

Data is transferred a serialized manner.

> `Serialization` is converting the data to byte stream for efficient data transfer.

> `Deserialization` is converting back from byte stream to data/object.


## Connect to a Database

> `Driver` is a software component that connects two dissimilar environments.

Each database vendor has to develop a `Driver` class that implements the `java.sql.Driver` interface of the `JDBC API`.

Java application can use that driver class to connect to the database.

To Connect to a database:
```java
static final String JDBC_DRIVER = "com.mysql.cj.jdbc.Driver"; 
//you can use com.mysql.jdbc.Driver as JDBC_DRIVER
// Registering the JDBC driver
Class.forName(JDBC_DRIVER);
//driver loading is automatically done in JDBC 9 or greater version

static final String DB_URL = "jdbc:mysql://localhost:3306/jdbc_demo";
static final String USER = "root";
static final String PASS = "infy";

// connection object controls the database
Connection connection = null;
connection = DriverManager.getConnection(DB_URL, USER, PASS);
```

## Run Quaries on the database

- the `Connection Object` is used to create statements
- the `Statement Object` is used to execute sql statements
- the `ResultSet Object` is returned and contains the reulst of the query

```java
Statement statement = null;
statement = connection.createStatement();

String sql;
sql = "select * from employee";
ResultSet resultset = statement.executeQuery(sql);
```