## WK1

### 1.1 What is the difference between assigning and declaring a variable?

### 1.2 What do a pair of opening and closing curly braces represent?

### 1.3 What is the difference between source code and bytecode?

- Compilation means to transform a program written in a high-level programming language from `source code` into `object code` / `bytecode`.
- `.java` -> `.class`

### 1.4 What is the difference in syntax between calling a method and creating a method?

### 1.5 What is a method?

Blocks of reusable code that can be invoked again and again.

### 1.6 What is a variable?

- container for storing data.
- types:
  - primitive type
  - reference type

### 1.7 What is the difference between the JDM, JRE, and JVM?

- `JVM` Programs that are written in Java are executed utilizing the Java Virtual Machine (JVM). The JVM is a special program that knows how to execute the programs that you write in Java
- `JRE` In order to run Java code, you also need a Java Runtime Environment (JRE), which contains all the runtime libraries that your code will be calling and using. The JRE contains the JVM within it
- `JDK`: JDK - Java Development Kit, which provides developer tools like a compiler, debugger, documentation tools, and other command-line utilities. The JDK also has a JRE inside of it

### 1.8 What is a conditional statement?

### 1.9 Explain the different kinds of loops you can create and use in a program.

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

### 1.10 Explain the main method.

```java
public class HelloWorld{
  public static void main(String[] args) {
    System.out.println("Hello, World!");
  }
}
```

### 1.11 What is a primitive datatype? Please list a few and explain them.

- data types defined by the language
- stores the value of the data
- types
  - boolean_1 bit_true or false
  - byte 1 byte numerical
  - char 2 bytes 1 character
  - short 2 bytes numerical
  - int 4 bytes numerical
  - float 4 bytes floating point
  - long 8 bytes numerical
  - double 8 bytes floating point

### 1.12 What is the modulo operator? How is it useful?

### 1.13 What are shorthand assignment operators?

= += -= \*= /= %= &= ^=

### 1.14 How do you use increment and decrement operators?

- postfix: changes the value after the entire expression is evaluated

```java
int a = 5;
int b = a++; // b=5, a=6
```

- prefix

```java
int a = 5;
int b = ++a; // b=6, a=6
```

### 1.15 How can you iterate over an array?

### 1.16 What is an array? Why is it useful?

### 1.17 What is a stacktrace? How can you use it to debug your application?

Each JVM thread (a path of execution) is associated with a stack that's created when the thread is created. This data structure is divided into frames, which are data structures associated with method calls. For this reason, each thread's stack is often referred to as a method-call stack.

When an exception / error gets thrown. A stack trace is displayed to the console.

### 1.18 What is the Scanner class used for? Give an example of how you would use it.

- The Scanner class is used to get user input, and it is found in the java.util package.

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
  }
}
```

### 1.19 When would you use an if statement over a switch statement?

- `switch` statement works with:
  - `byte`, `short`, `int`
  - `char`, `String`
  - `enum`
- if the if statement is too long switch can be better

### 1.20 When would you use a switch statement over an if statement?

### 1.21 What is an operating system?

- a software that communicates with the hardware and allows other programs to run

### 1.22 What does the term "full stack" mean?

### 1.23 Which datatype represents text in Java?

### 1.24 How would you access the last value in an array if you do not know the size of the array?

### 1.25 What steps would you take to debug your program if it crashed with an error message in the console?

### 1.26 What steps would you take to debug your program if runs, but gives you the wrong results?

### 1.27 How would you describe the compilation process for Java?

- 2 steps
  - compiler creates machine independent `bytecode`
  - `JVM` creates machine code

### 1.28 Give me an example of why you would need to create a method other than the main method.

### 1.29 Can you describe some of the basic entities of a Java program?

- Classes
- Variables
- Methods

### 1.30 What are some of the benefits of Java?

- platform independent,
- has a C-language inspired syntax
- provides automatic memory management
- has an extensive built-in runtime library
- is supported by the Oracle corporation
- has a rich open source community

### 1.31 What is a flow control statement?

- `if` execute a statement or a block of statements only if some conditional test turns out to be true
- `switch` execute one of several blocks of statements depending on the value of a variable of certain types
- loops: allow for the repeated execution of the same statement or block of statements

### 1.32 What is the modulo operator and why would we use it?

## WK 2

### 2.1 What is a package and why would we use one?

- a `package` is a collection of classes, interfaces, and enums in a hierarchial manner.
- why?
  - keep your classes separate from the classes in the Java API
  - reuse classes in other applications.
  - distribute your classes to others.

### 2.2 What is the difference between using an instance variable and a static variable?

### 2.3 What is the difference between calling an instance method and a static method?

### 2.4 What are classes used for?

### 2.5 Describe what an object is.

### 2.6 What is the role of garbage collection in Java?

Removing objects from the heap which have no references to them.

### 2.7 If I define a variable within a method, how can I access its value outside of the method?

### 2.8 Describe the difference between the stack and the heap.

#### `Stack` vs `Heap`

- static vs dynamic memory allocation
- fast vs. slow memory access
- `java.lang.StackOverFlowError` vs `java.lang.OutOfMemoryError`
- automatic memory flush vs garbage collection
- threadsafe vs not threadsafe

#### `Stack`

- `Stack` Memory in Java is used for static memory allocation and the execution of a thread. It contains primitive values that are specific to a method and references to objects referred from the method that are in a heap.
- Access to this memory is in Last-In-First-Out (LIFO) order.
- When the method finishes execution, its corresponding stack frame is flushed, the flow goes back to the calling method, and space becomes available for the next method.
- It grows and shrinks as new methods are called and returned, respectively.
- Variables inside the stack exist only as long as the method that created them is running.
- It's automatically allocated and deallocated when the method finishes execution.
- If this memory is full, Java throws java.lang.StackOverFlowError.
- Access to this memory is fast when compared to heap memory.
- This memory is threadsafe, as each thread operates in its own stack.

#### `HEAP`

- used for the dynamic memory allocation of Java objects and JRE classes at runtime.

### 2.9 What is a constructor and how is it different from a method?

Constructors:

- have no return types
- have same name as class
- provide no functionality to object
- called at object creation when a class is instanceated

### 2.10 What is the difference between an array and an ArrayList?

### 2.11 What is the difference between an Error and an Exception?

#### `Error`

Represents something that went so horribly wrong with your application that you should not attempt to recover from. Some examples of errors are:

- ExceptionInInitializerError
- OutOfMemoryError
- StackOverflowError

#### `Exception`

### 2.12 How would you handle an exception?

### 2.13 What is the difference between a checked and an unchecked exception?

### 2.14 If you received text input from the user, how would you go about comparing it to a value, like "yes" or "no"?

```java
String str1 = "yes";
String str2 = "no";
boolean isSame = str1.equals(str2);
```

### 2.15 What is explicit and implicit casting?

- `implicit casting`: Java is able to do this conversion automatically
- `explicit casting` with `()`:

```java
int i = 200;
short s = (short)i;
```

### 2.16 What are the different scopes in Java?

- Instance, or object, scope
- Class, or static, scope
- Method scope
- Block scope

### 2.17 What is autoboxing and unboxing?

- `Boxing` is the process of converting a primitive to its wrapper class. Java has a feature called `autoboxing`which will automatically convert primitives to wrapper classes implicitly. In case when passing an `int` variable as parameter to a function requesting an `Integer`.
- `Unboxing` is the reverse - converting a wrapper class to its primitive.

### 2.18 If there was an error in the console when you tried to run your program, how would you debug?

### 2.19 What are some operations you can perform on a List?

- `add`, `remove`, `get`, `set`
- `.indexOf()`, `.lastIndexOf()`
- `sublist`
- `sort`, `reverse`, `rotate`, `swap`
- `replaceAll`, `fill`, `copy`
- `indexOfSubList`, `lastIndexOfSublist`

## WK 3

### 3.1 Describe inheritance and how would you use it in a project?

`Inheritance` is inheriting the common state and behavior of parent class (super class) by its derived class (sub class or child class).
A sub class can inherit all non-private members from super class, by default.

Types:

- `single`
- `multi-level`
- `hierarchical`: one super class with more than one subclasses
- `multiple`: inherit from more than one parent (NOT POSSIBLE IN JAVA)

Example:
Animal -> Cat, Dog

### 3.2 Describe abstraction and how would you use it in a project?

`Abstraction` is a programming principle in which we hide underlying complexity through a simplified interface.

### 3.3 Describe polymorphism and how would you use it in a project?

`polymorphism` means "taking on many forms". In OOP polymorphism provides the means to perform a single action in multiple different ways

The most common examples of polymorphism:

- method overloading
- method overriding
- upcasting
- downcasting

#### `method overloading`

Within a class when there are two or more methods in a class with the same method name, but different method signatures by changing the parameter list.

- change in number of parameters
- change in types of parameters
- compile time / static polymorphism

#### `method overriding`

when a method in a child class has the same method signature as a method in the parent class, but with a different implementation

- make class hierarchies more flexible and dynamic
- runtime / dynamic polymorphism
- `static methods` cannot be overriden
- return type can only be changed if it is a subtype of the original type (`covariant return types`)
- access modifier can be changed but must provide more _not less_ access

`virtual method invocation` when variable is declared as type Animal but refers to a Dog object, calling the method spead will use Dog's implementation of the method

#### `upcasting`

is the process of casting an object of a subclass to an object of its superclass

- done automatically by the Java compiler
- safe operation does not involve loss of data
- you can access only the members of the superclass, but don not lose any members of the subclass

#### `downcasting`

The process of casting an object of a superclass to an object of its subclass

- risky, may result in `ClassCastException` if the object being cast is not actually an instance of the subclass
- use `instanceof` operater to check before downcasting

### 3.4 Describe encapsulation and how would you use it in a project?

- `encapsulation` is a process of wrapping data and methods in a single unit.
- it is an OOP principle
- in OOP data and methods operating on that data are combined together to form a single unit, which is referred to as a Class
- `encapsulation` is as a protective wrapper that prevents the code and data from being arbitrarily accessed by other code defined outside the wrapper.

> `encapsulation` means **restricting access to data members** by using access modifiers and getter/setter methods

### 3.5 How is method overriding different from method overloading?

### 3.6 What are the four levels of access we can give to class members? How are they different from one another?

- `access modifiers` set access level of methods, variables, classes and constructors

Types:

- `public`: can be accessed by any classes
- `default` (when there is no access modifier): within the same package only
- `protected`: within package + outside of package through inheritance
- `private`: only within the class, a class (except a nested class) cannot be private

### 3.7 What is the purpose of using getter and setter methods?

### 3.8 Why would you use an interface over an abstract class?

Interfaces have these advantages over class:

- Implementation details do not need to be provided in the interface.
- A class can only extend one other class, but it can implement as many interfaces as needed.

### 3.9 What methods are commonly overridden from the Object class and why?

- `equals()`
- `hashCode()`
- `toString()`

In Object class `equals()` is true if we compare the same instance, for value objects we may want to compare based on property values.

- two instances of _Person_ with same name and birthday should be different
- we may want to two instances of _Money_ with same ammount and currancy be the same, in this case we have to change both the `equals()` and `hashCode()` methods

### 3.10 What state and behavior would you define in a parent class but not a subclass?

### 3.11 What state and behavior would you define in a subclass but not in the parent class?

### 3.12 What are the SOLID design principles and are they important?

- `Single Responsibility Principle (SRP)`: A class should have only one purpose, focusing on a single responsibility or task.
- `Open-Closed Principle (OCP)`: Software entities should be open for extension but closed for modification, enabling flexibility and avoiding modification of existing code.
- `Liskov Substitution Principle (LSP)`: Objects of a superclass should be replaceable with objects of their subclasses without effecting the consistency of the program's behavior.
- `Interface Segregation Principle (ISP)`: Clients should not be forced to depend on interfaces they do not use, emphasizing specific interfaces tailored to clients' needs and reducing unnecessary dependencies.
- `Dependency Inversion Principle (DIP)`: High-level modules should not depend on low-level modules; both should depend on abstractions, promoting loose coupling and dependency inversion through abstractions.

### 3.13 What is Maven? Why would we use it?

`Maven` is a tool that can be used for building and managing any Java-based project.

- A build automation and dependency management tool for Java. Maven project configuration and dependencies are handled via the `Project Object Model`, defined in the `pom.xml` file.
- A testing framework
- A logging library which allows for multiple logging thresholds
- A library of tools for adding functionality to a Java application

### 3.14 What is the SDLC? Why is it important?

`SDLC` `Software Delevopment Life Cycle`

Helps companies:

- reduce cost
- deliver software faster
- meet or exceed customer satisfaction

Stages of SDLC:

- Planning
- Define Requirements
- Design and Prototyping
- Software Development
- Testing
- Deployment
- Operation & Maintenance

### 3.15 When would you use an Agile methodology versus Waterfall?

- when i want to see results faster
- when i want to be flexible
<hr>

#### Waterfall

##### The advantages of waterfall

- Requires less coordination due to clearly defined phases sequential processes
- A clear project phase helps to clearly define dependencies of work.
  The cost of the project can be estimated after the requirements are defined
- Better focus on documentation of designs and requirements
  The design phase is more methodical and structured before any software is written

##### The disadvantages of waterfall

- Harder to break up and share work because of stricter phase sequences teams are more specialized
- Risk of time waste due to delays and setbacks during phase transitions
  Additional hiring requirements to fulfill specialized phase teams whereas agile encourages more cross-functional team composition.
- Extra communication overhead during handoff between phase transitions
- Product ownership and engagement may not be as strong when compared to agile since the focus is brought to the current phase.

#### Agile

##### The advantages of agile project management

- Faster feedback cycles
  Identifies problems early
- Higher potential for customer satisfaction
- Time to market is dramatically improved
- Better visibility / accountability
- Dedicated teams drive better productivity over time
- Flexible prioritization focused on value delivery

##### The disadvantages of agile

- Critical path and inter-project dependencies may not be clearly defined as in waterfall
- There is an organizational learning curve cost
- True agile execution with a continuous deployment pipeline has many technical dependencies and engineering costs to establish

### 3.16 What is test driven development?

The `TDD` process consists of writing unit tests first, **before** the implemented application code has been written.

`Unit testing` is the testing of individual software components in isolation from the rest of the system.

### 3.17 Why are unit tests important?

When refactoring code, the unit tests give us confidence that we can change the source code without breaking existing functionality. This makes debugging much easier.

### 3.18 How can JUnit annotations help with running our tests?

`Annotations` are used to support, identify, and execute test method features.

- `@BeforeAll`
- `@BeforeEach`
- `@AfterEach`
- `@AfterAll`
- `@Test`

### 3.19 What are the Maven build lifecycle phases?

The phases of the build lifecycle are:

- `validate`: validate the project is correct and all necessary information is available
- `compile`: compile the source code of the project
- `test`: test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
- `package`: take the compiled code and package it in its distributable format, such as a JAR.
- `verify` - run any checks on results of integration tests to ensure quality criteria are met
- `install` - install the package into the local repository, for use as a dependency in other projects locally
- `deploy` - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.

### 3.20 Describe the POM.xml file and its importance.

`POM` - `Project Object Model`

`Maven` identifies projects through project coordinates defined in the pom.xml file - these are:

- `group-id`: company name for example: "com.revature"
- `artifact-id`: project name
- `version`: version number for example: "0.0.1-SNAPSHOT"

Together, these uniquely identify a specific version of a program.

#### Some other important tags within the `pom.xml` file include:

`<project>` - this is the root tag of the file

- `<modelVersion>` - defining which version of the page object model to be used
- `<name>` - name of the project
- `<properties>` - project-specific settings
- `<dependencies>`: this is where you put your Java dependencies you want to use. Each one needs a
  - `<dependency>` which has:
    - `<groupId>`
    - `<artifactId>`
    - `<version>`
- `<plugins>` for 3rd party plugins that work with Maven

Here's an example:

```xml
<project>
  <modelVersion>4.0.0</modelVersion>

  <groupId>com.revature.app</groupId>
  <artifactId>my-app</artifactId>
  <version>1</version>

  <dependencies>
    <dependency>
      <groupId>org.apache.maven</groupId>
      <artifactId>maven-artifact</artifactId>
      <version>${mavenVersion}</version>
    </dependency>
    <dependency>
      <groupId>org.apache.maven</groupId>
      <artifactId>maven-core</artifactId>
      <version>${mavenVersion}</version>
    </dependency>
  </dependencies>

</project>
```

## WK 4

### 4.1 What is SQL and why would we use this language

`Structured Query Language` (`SQL`) is the language used to administer SQL-based RDBM systems.

### 4.2 What are the SQL sublanguages and their purpose?

- `DDL` Data Definition Language. Defines data structure
  - `CREATE`
  - `ALTER`
  - `DROP`
  - `TRUNCATE`
  - `RENAME`
  - COMMENT:
    - single line `--`
    - multi-line `/**/`
- `DML` Data Manipulation Language
  - `INSERT`
  - `UPDATE`
  - `DELETE`
- `DCL` Data Control Language - manage access permissons to database object
  - `GRANT`
  - `REVOKE`
- `TCL` Transaction Control Language. Defines concurrent operation boundaries
  - `COMMIT`
  - `ROLLBACK`
  - `SAVEPOINT`
- `DQL` Data Query Language. Search, filter, group, aggregate stored data
  - `SELECT`

### 4.3 What is a RDBMS?

- An RDBMS is a data storage system based on a relational model
- data that is related to a particular object is stored in tables with each entry being represented as a row
- and each data point is a column in the row that is validated by a set of constraints

### 4.4 Describe relational database tables.

In MySQL, a table stores and organizes data in columns and rows as defined during table creation.

### 4.5 What are constraints and can you describe a few constraints?

`Constraints` are used to define a database schema and are the backbone for defining `integrity constraints` of the schema. They help validate data beyond just a simple data type.

- `NOT NULL` Ensures that a column's value is not null.
- `UNIQUE` Ensures that a column's value is unique in the table. (Can have one `NULL` value.)
- `PRIMARY KEY` Combines unique and not null. Uniquely identifies each row.
- `FOREIGN KEY` Links to a row in another table. Prevents the destruction of those links.
- `DEFAULT` Specifies a value for a column, if one is not given.
- `CHECK`
  - helps us to get only those values that are valid for the condition and our requirements.
  - ``
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

### 4.6 Why would I use the WHERE clause?

FILTERING: The filtering clause of a select statement is a `WHERE` clauses that defines how selected rows are filtered from the table. `WHERE` clauses use logical operators to select records that meet specific conditions.

### 4.7 What are some operators that can be used in SQL?

- Arithmetic
- Bitwise
- Comparison
- Compound
- Logical

### 4.8 What is the JDBC API and the benefits of using it?

`JDBC` stands for `Java Database Connectivity`. It is a relatively low-level API used to write Java code that interacts with relational databases via SQL.

Benefit: It is database agnostic. It uses database drivers which implement the interfaces defined in the JDBC API for the given database.

In order to interact with a database, we need to do several things:

#### Register the JDBC driver

Many JDBC drivers are available through `Maven`'s central repository and can be added as a dependency in the `pom.xml` file. (Oracle is an exception.)

#### Open a connection using

- We can use the DriverManager class to get a Connection to the database, given that we have the JDBC URL, username, and password.
- Generally these parameters should be stored in an external configuration file that can be loaded dynamically and changed without affecting the application code.
  -JDBC String
  The database `URL` is an address pointing to the database to be used, also known as the `JDBC String`. The format of this URL varies between database vendors, as shown in the table below:
- It's always a good idea to close your resources - below the try-with-resources syntax is used to automatically close the Connection being created after the block ends.

```java
try (Connection conn = DriverManager.getConnection(DB_URL,USERNAME,PASSWORD)) {
  // more code goes here
} catch (SQLException e) {}
```

- Autocommit mode
  By default, when a connection is created it is in auto-commit mode, so every SQL statement acts as a transaction and is committed immediately after execution. In order to manually group statements into a transaction, simply call:

```java
Connection conn = DriverManager.getConnection(DB_URL,USERNAME,PASSWORD);
conn.setAutoCommit(false);

// execute some SQL statements...
con.commit();
```

#### Execute SQL statements

The results that are returned in a `ResultSet` object.

##### Statement

Once we have the Connection object, we can write our SQL and execute it:

```java
Statement stmt = conn.createStatement();
String sql = "SELECT * FROM employees";
ResultSet rs = stmt.executeQuery(sql);
```

##### PreparedStatement

Alternatively, a `PreparedStatement` can be used. This interface gives us the flexibility of specifying parameters with the `?` symbol. It also **protects against SQL injection** when user input is used by pre-compiling the SQL statement.

```java
PreparedStatement ps = conn.prepareStatement();
String sql = "SELECT * FROM employees WHERE age > ? AND location = ?";
ps.setInt(1, 40);
ps.setString(2, "New York");
ResultSet rs = ps.executeQuery(sql);
```

##### CallableStatement

> The Statement and PreparedStatement also have additional methods for sending SQL, including:

- `.execute()` - for any kind of SQL statement, returns a boolean
- `.executeUpdate()` - for DML statements, returns an int which is the number of rows affected

#### Retreiving Results

Results from an SQL query are returned as a `ResultSet``, which can be iterated over to extract the data:

```java
List<Employee> empList = new ArrayList<>();
while (rs.next()) {
  int id = rs.getInt("id");
  String name = rs.getString("first_name");
  empList.add(new Employee(id, name));
}
```

### 4.9 What is the DAO Design Pattern and why should we use it?

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

### 4.10 What information would you need in order to successfully connect to a database?

- URL (`JDBC String`)
- username
- password

## WK 5

### 5.1 What is the difference between a Simple and Prepared JDBC statement?

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

### 5.2 What is SQL Injection and how can we prevent it using the JDBC?

### 5.3 What is a foreign key?

### 5.4 What is referential integrity?

### 5.5 What is normalization?

### 5.6 What is multiplicity?

### 5.7 Describe what a join is and explain the different types of joins we can create.

### 5.8 What is the difference between a join and a set operation?

### 5.9 What is a view and why is it useful?

### 5.10 What is HTTP? Why is it important to know about?

### 5.11 What are common HTTP verbs used when a client application is making a request?

### 5.12 What are some common HTTP status codes that can be included in a response?
