sql: 1-25

## SQL

### 1 What is a RDBMS?

### 2 What is SQL and why would we use this language

### 3 What are the SQL sublanguages and their purpose?

### 4 tables Describe relational database tables.

### 5 What are constraints and can you describe a few constraints?

### 6 Why would I use the WHERE clause?

### 7 What are some operators that can be used in SQL?

### 8 What is a foreign key?

### 9 What is referential integrity?

### 10 What is normalization?

### 11 What is multiplicity?

### 12 Describe what a join is and explain the different types of joins we can create.

### 13 What is the difference between a join and a set operation?

### 14 What is a view and why is it useful?

### 15 What is DCL?

### 16 What is TCL?

### 22 What is a transaction?

### 17 What is the difference between an aggregate and a scalar function?

### 23 What are the properties of a transaction?

### 24 What is a function in SQL?

Work on below

### 18 What is the GROUP BY clause used for?

### 19 What is the ORDER BY clause used for?

### 20 What is a stored procedure in SQL?

### 21 What is a trigger in SQL?

### 25 What is an index in SQL?

<hr>
<hr>
<hr>

# EDIT BELOW

## 1 operating system

## 2 Java compilation process

## X Java Entities

## 3 Java variables

## 4 Java data types

## 5 Java methods

## 6 Java main method

## x Java Conditionals

## x Java Loops

## x Scanner class

## X Arrays

## X String Class

EDIT BELOW

### 12 What is the modulo operator? How is it useful?

### 13 What are shorthand assignment operators?

Assgnment operators assign value to a variable.

= += -= \*= /= %= &= ^=

### 14 How do you use increment and decrement operators?

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

### 17 What is a stacktrace? How can you use it to debug your application?

> `Stack trace` is a report of the active `stack frames` at a certain point in time during a thread's execution.

Each `JVM thread` (a path of execution) is associated with a stack that's created when the thread is created.

This data structure (stack) is divided into `frames`, which are data structures associated with method calls. For this reason, each thread's stack is often referred to as a method-call stack.

When an exception / error gets thrown. A stack trace is displayed to the console.

### 25 debug crash What steps would you take to debug your program if it crashed with an error message in the console?

### 26 debug wrong result What steps would you take to debug your program if runs, but gives you the wrong results?

### 32 What is the modulo operator and why would we use it?

### 33 What is a package and why would we use one?

- a `package` is a collection of classes, interfaces, and enums in a hierarchical manner.
- why?

  - keep your classes separate from the classes in the Java API
  - reuse classes in other applications.
  - distribute your classes to others.

- naming convention: lowercase characters separated by periods in the reverse way you would specify a web domain (com.revature.mypackage)

- usage
  - by default, everything in the `java.lang` package is imported.
  - classes can be referenced anywhere in a program by their "fully qualified class name" - which is the package declaration followed by the class, in order to uniquely identify the class
  - using imports
- declare package: the first (non-commented) line in a .java file
  declares the package in which the class will reside.

```java
// declare the package this class belongs to
package com.revature.mypackage;

// import other packages to use
import java.util.*;
```

### 34 instance vs. static variable What is the difference between using an instance variable and a static variable?

The static keyword in Java is mainly used for memory management. The static keyword in Java is used to share the same variable or method of a given class.

When a member is declared static, it can be accessed before any objects of its class are created, and without reference to any object.

A static variable is a variable of a class that isn’t associated with an instance of a class.

Instead, the variable belongs to the class itself.

As a result, you can access the static variable without first creating a class instance.

### 35 instance vs. static method What is the difference between calling an instance method and a static method?

A static method is a method of a class that isn’t associated with an instance of a class.

Instead, the method belongs to the class itself.

As a result, you can access the static method without first creating a class instance.

### 36 What are classes used for?

A class is a template used to instantiate objects.

A class used as the `type` for a `reference variable` determines what behaviors of an object can be invoked, and how any variables get initialized.

We use classes to create a blueprint for objects.

### 37 Describe what an object is.

An object is an instance of a class in memory.

- In Java, you never interact with objects directly. Instead, you interact with them through their reference, which is the memory address used by the JVM to find a particular object.

- constructor declares how an object is to be instantiated and initialized from the class "blueprint".

### 38 What is the role of garbage collection in Java?

Garbage collection is the process of removing objects from the heap which have no references to them.

Garbage collection is run in the background by the JVM. There is no way we can explicitly force garbage collection to happen, but we can request garbage collection to be run through the use of one of the following:

- System.gc()
- Runtime.getRuntime().gc()
- System.runFinalize()

### 39 If I define a variable within a method, how can I access its value outside of the method?

When a variable is declared in a Java program, it is attached to a specific scope within the program, which determines where the variable resides. The different scopes of a variable in Java are:

- `Instance, or object scope` - The variable is attached to individual objects created from the class.
- `Class, or static scope` - Resides on the class definition itself.
- `Method scope` - Declared within a method block; only available within the method in which they are declared.
- `Block scope` - Only exist within the specific control flow block (for, while, etc.)

### 40 stack vs. heap Describe the difference between the stack and the heap.

To run an application in an optimal way, JVM divides memory into stack and heap memory. Whenever we declare new variables and objects, call a new method JVM designates memory to these operations from either Stack Memory or Heap Space.

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
- If this memory is full, Java throws `java.lang.StackOverFlowError`.
- Access to this memory is fast when compared to heap memory.
- This memory is threadsafe, as each thread operates in its own stack.

#### `HEAP`

- used for the dynamic memory allocation of Java objects and JRE classes at runtime.

<table>
<thead>
<tr>
<td>Parameter</td>	<td>Stack Memory</td>	<td>Heap Space</td></tr>
</thead>
<tbody>
<tr>
<td>Application</td>
<td>Stack is used in parts, one at a time during execution of a thread</td>
<td>The entire application uses Heap space during runtime</td>
</tr>
<tr>
<td>Size</td>
<td>Stack has size limits depending upon OS, and is usually smaller than Heap</td>
<td>There is no size limit on Heap</td>
</tr>
<tr>
<td>Storage</td>
<td>Stores only primitive variables and references to objects that are created in Heap Space</td>
<td>All the newly created objects are stored here</td>
</tr>
<tr>
<td>Order</td>
<td>It's accessed using Last-in First-out (LIFO) memory allocation system</td>
<td>This memory is accessed via complex memory management techniques that include Young Generation, Old or Tenured Generation, and Permanent Generation.</td>
</tr>
<tr>
<td>Life</td>
<td>Stack memory only exists as long as the current method is running</td>
<td>Heap space exists as long as the application runs</td>
</tr>
<tr>
<td>Efficiency</td>
<td>Much faster to allocate when compared to heap</td>
<td>Slower to allocate when compared to stack</td>
</tr>
<tr>
<td>Allocation/Deallocation</td>
<td>This Memory is automatically allocated and deallocated when a method is called and returned, respectively</td>
<td>Heap space is allocated when new objects are created and deallocated by Garbage Collector when they're no longer referenced</td>
</tr>
</tbody>

</table>

### 41 What is a constructor and how is it different from a method?

A `constructor` is a special method that declares how an object is to be instantiated and initialized from the class "blueprint".

- A constructor is declared like a method, except its method signature does not contain a return type, and a constructor always has the same name as the class.

- The new object created by the constructor is always of the class in which the constructor is declared.
  this refers to the object which is being instantiated - it is used to initialize instance variables, or - to call other constructors (this is called constructor chaining)
  There is another keyword important for constructors - the super keyword, which references the "super", or parent, class.
  When invoked as a method (super()), the parent class constructor will be called.
  A super() call (or a this() call) must be the first line of any constructor.
- If not explicitly provided, the compiler will inject super() it on the first line implicitly.
  The "default" constructor takes no arguments and simply calls super() (see above) - sometimes it is referred to as the "default, no-args" constructor.
- However if we define our own constructor(s) in the class, we will not receive a default constructor from the compiler.

#### Constructors vs. Methods

- have no return types
- have same name as class
- provide no functionality to object
- automatically called at object creation when a class is instanceated

### 42 array vs. ArrayList What is the difference between an array and an ArrayList?

### 43 Error vs. Exception What is the difference between an Error and an Exception?

Both `Error` and `Exception` extend the `Throwable` class

#### `Error`

1. `Compilation Error`

- occurs at compile time
- syntax error
- not handling checked exceptions
- eg: `SyntaxError`

2. `Error`

- occurs at runtime
- severe problem with the program
- we dot hand attempt to recover from them
- eg: `OutOfMemoryError`

#### `Exception`

Exceptions are the conditions that occur at runtime and may cause the termination of the program. But they are recoverable using try, catch and throw keywords.

- can be recovered from with `try - catch`
- two types
  - checked
    - must be handled
    - eg: `IOException`
  - unchecked
    - runtime errors
    - eg: `ArrayOutOfBounds`

### 44 handle exceptions How would you handle an exception?

When risky code is written that has the possibility of throwing an exception, it can be dealt with in one of two ways:

1. `Handling` means that the risky code is placed inside a `try/catch` block
2. `Declaring` means that the type of exception to be thrown is listed in the method signature with the throws keyword. This is also called "ducking" the exception - you let the code which calls the method deal with it.

If the exception is not handled anywhere in the program, it will propagate up through the call stack until it is handled by the JVM which then terminates the program.

### 45 checked vs. unchecked exception What is the difference between a checked and an unchecked exception?

- Checked exception require mandatory handling:

  - try - catch
  - throws

- Handling the exception is checked during compilation, gives compliation error if not handled.

- Exception-handling is mandatory for any exception class that is not a subclass of either Error or RuntimeException.

### 46 compare strings If you received text input from the user, how would you go about comparing it to a value, like "yes" or "no"?

```java
String str1 = "yes";
String str2 = "no";
boolean isSame = str1.equals(str2);
```

### 47 casting What is explicit and implicit casting?

`Casting` is the process of converting a data type to another data type.

`implicit casting`

- automatically done by Java
- does it with primitive data types
- where there is no loss of data

  - If one of the values is a double, the other value is converted to a double
  - If neither is a double but one is a float, the other is converted to a float.
  - If neither is a double nor a float but one is a long, the other is converted to a long.
  - If all else fails, both values are converted to int.

`explicit casting`

- done by programmer
- uses `()`:

```java
int i = 200;
short s = (short)i;
```

- In some cases you will have to use the data type's own methods to convert. Some of these methods are listed in the table below.
  - `String` to `int` with `Integer.parseInt(String)`
  - `int` to `String` with `String.valueOf(int)`

### 48 scopes What are the different scopes in Java?

- Instance, or object, scope
- Class, or static, scope
- Method scope
- Block scope

### 49 What is autoboxing and unboxing?

- `Boxing` - the process of converting a primitive to its wrapper clas
- `autoboxing` - Java feature which will automatically convert primitives to wrapper classes implicitly. In case when passing an `int` variable as parameter to a function requesting an `Integer`.
- `Unboxing` is the reverse - converting a wrapper class to its primitive.
- Wrapper classes have static helper methods like .parseX() and .valueOf() for explicit primitive conversion.

### 50 If there was an error in the console when you tried to run your program, how would you debug?

### 51 list operations What are some operations you can perform on a List?

`List`

- interface
- implements collection interface
- collection of elements of the same type
- preserves the order in which elements are inserted
- duplicate entries are allowed
- elements are accessed by their index, which begins with 0

List interface includes operations:

- positional access operations
- search operations
- iteration operations
- range-view operations

#### 1. Positional access operations

Manipulates elements based on their numerical position in the list

- `get`
- `set`
- `add`
- `addAll`
- `remove`

#### 2. Search operations

Searches for a specified object in the list and returns its numerical position.

- `.indexOf()` -`.lastIndexOf()`
- `indexOfSubList`

#### 3. Iteration operations

`ListIterator`, which allows you to traverse the list in either direction, modify the list during iteration, and obtain the current position of the iterator.

Methods:

Inherited from `Iterator`

- `hasNext()`
- `next()` - moves cursor forward
- `remove()`

Added methods:

- `hasPrevious()`
- `previous()` - moves cursor backward

```java
// iterating backwards through a  List
for (ListIterator<Type> it = list.listIterator(list.size()); it.hasPrevious(); ) {
    Type t = it.previous();
    ...
}
```

Arguments

The List interface has two forms of the listIterator method.

- no arguments: returns a ListIterator positioned at the beginning of the list
- with an int argument: returns a ListIterator positioned at the specified index.

The index refers to the element that would be returned by an initial call to next. An initial call to previous would return the element whose index was index-1. In a list of length n, there are n+1 valid values for index, from 0 to n, inclusive.

Cursor

- Intuitively speaking, the `cursor` is always between two elements — the one that would be returned by a call to previous and the one that would be returned by a call to next
- Calls to next and previous can be intermixed, but you have to be a bit careful. The first call to previous returns the same element as the last call to next. Similarly, the first call to next after a sequence of calls to previous returns the same element as the last call to previous.

#### 4. Range-view operations

Returns a List view of the portion of this list whose indices range from fromIndex, inclusive, to toIndex, exclusive.

The returned List is backed up by the List on which subList was called, so changes in the former are reflected in the latter.

- `sublist(int fromIndex, int toIndex)`

### 52 Describe inheritance and how would you use it in a project?

`Inheritance` is inheriting the common state and behavior of parent class (super class) by its derived class (sub class or child class).
A sub class can inherit all non-private members from super class, by default.

Types:

- `single`
- `multi-level`
- `hierarchical`: one super class with more than one subclasses
- `multiple`: inherit from more than one parent (NOT POSSIBLE IN JAVA)

Example:
Animal -> Cat, Dog

```java
class Animal {
  ...
}

class Dog extends Animal {
  ...
}
```

### 53 Describe abstraction and how would you use it in a project?

`Abstraction` is an OOP programming principle.

Through abstraction we hide underlying complexity through a simplified interface.

example: Shape class, getArea() method

### 54 Describe polymorphism and how would you use it in a project?

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

EXAMPLE
method overloading - temperature converter working with both integers, doubles or string

method overriding - speak method implemented differently in Animal subspecies

### 55 Describe encapsulation and how would you use it in a project?

- `encapsulation` is a process of wrapping data and methods in a single unit.
- it is an OOP principle
- in OOP data and methods operating on that data are combined together to form a single unit, which is referred to as a Class
- `encapsulation` is as a protective wrapper that prevents the code and data from being arbitrarily accessed by other code defined outside the wrapper.

> `encapsulation` means **restricting access to data members** by using access modifiers and getter/setter methods

When encapsulating your code, certain conventions should be followed:

- All instancce fields for a class should be private
- Each field should have getters and setters as needed (typically these are public, but other access modifiers can be used as needed).
- Getter and Setter Methods (a.k.a. 'accessor' and 'mutator' methods) should use the following name convention:
  - getVariableName
  - setVariableName

EXAMPLE
employee object, make slary private, setSalary checks valid salary number, getSalary check is user has access rights

### 56 How is method overriding different from method overloading?

### 57 access modifiers What are the four levels of access we can give to class members? How are they different from one another?

- `access modifiers` set access level of methods, variables, classes and constructors

Types:

- `public`: can be accessed by any classes
- `default` (when there is no access modifier): within the same package only
- `protected`: within package + outside of package through inheritance
- `private`: only within the class, a class (except a nested class) cannot be private

### 58 What is the purpose of using getter and setter methods?

### 59 Why would you use an interface over an abstract class?

Interfaces have these advantages over class:

- Implementation details do not need to be provided in the interface.
- A class can only extend one other class, but it can implement as many interfaces as needed.

### 60 object methods to override What methods are commonly overridden from the Object class and why?

- `equals()`
- `hashCode()`
- `toString()`

#### `toString()`

The `toString()` method is automatically called if you print an Object. Usually, this is overridden to provide human-readable output. Otherwise, you will print out fully.qualified.ClassName@memoryAddress

#### `equals(Object o)`

The `equals(Object o)` method compares two Objects. The == operator also compares objects, but only the memory address (i.e. will return true if and only if the variables refer to the exact same object in memory). By default, and unless you explicitly override it, the equals method simply calls the == operator.

In Object class `equals()` is true if we compare the same instance, for value objects we may want to compare based on property values.

- two instances of _Person_ with same name and birthday should be different
- we may want to two instances of _Money_ with same amount and currency be the same, in this case we have to change both the `equals()` and `hashCode()` methods

#### `hashCode()`

The `hashCode()` method returns a hash code - a number that puts instances of a class into a finite number of categories.

There are a few rules that the method follows:

- You are expected to override hashCode() if you override equals()
- The result of hashCode() should not change in a program
- if .equals() returns true, the hash codes should be equal
- if .equals() returns false, the hash codes do not have to be distinct. However, doing so will help the performance of hash tables.

#### `.finalize()` _DEPRECIATED_

Finally, the `.finalize()` method is called by the garbage collector when it determines there are no more references to the object. It can be overriden to perform cleanup activities before garbage collection, although it has been deprecated in newer versions of Java.

### 61 What state and behavior would you define in a parent class but not a subclass?

Example:
Animal:
age, name, abstract makeNoise, sleep

### 62 What state and behavior would you define in a subclass but not in the parent class?

Example
Animal:
age, name, abstract makeNose, sleep
Dog: growl

### 63 What are the SOLID design principles and why are they important?

- SRP - Single Responsibility Principle
- OCP - Open Closed Principle
- LSP - Liskov Substitution Principle
- ISP - Interface Segregation Principle
- DIP - Dependency Inversion Principle

#### `Single Responsibility Principle (SRP)`

- A class should have only one purpose, focusing on a single responsibility or task.
- EXAMPLE: pulling data from a server, manipulating and storing it in a database is not single responsibility

#### `Open-Closed Principle (OCP)`:

- Software entities should be open for extension but closed for modification
- you should be able to **add new functionality
  to a system without modifying its existing** code
- we use `abstract classes` and `interfaces` to achieve the `Open Close Principle`
- EXAMPLE: have an abstract area method in a shape class, that can be implemented differentle in triangles and squares, rather than if statements in shape class that have to be modified any time a new shape is introduced

#### `Liskov Substitution Principle (LSP)`

- Objects of a superclass should be replaceable with objects of their subclasses
- any instance of a base class should be able to be replaced by an instance of a subclass without affecting the correctness of the program
- This means that, given that class B is a subclass of class A, we should be able to pass an object of class B to any method that expects an object of class A and the method should not give any weird output in that case.
- This is the expected behavior, because when we use inheritance we assume that the child class inherits everything that the superclass has. The child class extends the behavior but never narrows it down.
- EXAMPLE:

#### `Interface Segregation Principle (ISP)`

- is about separating interfaces, many client-specific interfaces are better than one general-purpose interface
- Clients should not be forced to depend on interfaces they do not use
- EXAMPLE vehicle interface with opendoors() method and Bike class implementing vehicle interface and mock implement opendoors() method

#### `Dependency Inversion Principle (DIP)`

- our classes should depend upon interfaces or abstract classes instead of concrete classes and functions
- if the `OCP (Open Closed Principle)` is the goal of `OO` architecture, `DIP (Dependency Inversion Principle)` is the primary mechanism to achive it

### 64 What is Maven? Why would we use it?

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

### 65 What is the SDLC? Why is it important?

The `Software Delevopment Life Cycle` (`SDLC`)
is the application of **standard business practices** to building software applications.

Helps companies:

- reduce cost
- deliver software faster
- meet or exceed customer satisfaction

Stages of SDLC:

- `Planning` - define the scope and purpose of the application.
- `Requirements` - part of planning, includes defining the resources needed to build the project
- `Design` - models the way a software application will work: architecture, user interface, platforms, programming, communications, security, may include `prototyping`
- `Build` - actual writing of the program
- `Document` - may include user guides, troubleshooting guides, and FAQ’s
- `Test`
- `Deploy`
- `Maintain`

### 66 agile vs. waterfall When would you use an Agile methodology versus Waterfall?

- when i want to see results faster
- when i want to be flexible

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

## Using a Database in Java

### 79 What is the JDBC API and the benefits of using it?

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

##### Statement

```java
Statement stmt = conn.createStatement();
String sql = "SELECT * FROM employees";
ResultSet rs = stmt.executeQuery(sql);
```

##### PreparedStatement

```java
PreparedStatement ps = conn.prepareStatement();
String sql = "SELECT * FROM employees WHERE age > ? AND location = ?";
ps.setInt(1, 40);
ps.setString(2, "New York");
ResultSet rs = ps.executeQuery(sql);
```

- pre-compiled SQL statement
- protects against SQL injection

> The Statement and PreparedStatement also have additional methods for sending SQL, including:

- `.execute()` - for any kind of SQL statement, returns a boolean
- `.executeUpdate()` - for DML statements, returns an int which is the number of rows affected

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

### 80 What is the DAO Design Pattern and why should we use it?

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

### 81 What information would you need in order to successfully connect to a database?

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

### 82 statement vs. preparedStatement What is the difference between a Simple and Prepared JDBC statement?

Once we have the `Connection object`, we can write our SQL and execute it.

#### `Statement`

The `Statement interface` is used for executing static SQL statements.

```java
Statement stmt = conn.createStatement();
String sql = "SELECT * FROM employees";
ResultSet rs = stmt.executeQuery(sql);
```

#### `Prepared Statement`

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

### 83 What is SQL Injection and how can we prevent it using the JDBC?

`SQL Injections` are the exploitation of programming weaknesses in SQL codes to gain access to a database, its resources, and applications.

`PreparedStatement` can be used to prevent SQL injections.

```java
PreparedStatement ps = conn.prepareStatement();
String sql = "SELECT * FROM employees WHERE age > ? AND location = ?";
ps.setInt(1, 40);
ps.setString(2, "New York");
ResultSet rs = ps.executeQuery(sql);
```

- specify parameters with the ? symbol
- protects against SQL injection when user input is used by pre-compiling the SQL statement

## HTTP

### 91 What is HTTP? Why is it important to know about?

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

### 92 What are common HTTP verbs used when a client application is making a request?

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

### 93 What are some common HTTP status codes that can be included in a response?

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

# WK 6

## 94 What is a functional interface and why would we use one?

functional interfaces

## 95 What is a lambda? Give an example of how we can use one.

lambda

## 96 What is a method reference?

method references

## 97 Describe Javalin.

Javalin

## 98 What is JSON? When would we work with JSON in our application?

JSON

## 99 What is a handler?

handler

## x Logging

## x What is Mockito and why would we use it?

## x What is a mock?

EDIT BELOW

## 103 What is REST and what are its key constraints?

## 105 REST naming URL What are some best practices for naming resource URLs using REST?

## 106 What is an endpoint?

wk7

What is a Collection?
What is the Collection API?
What are the major differences between a List, Queue, Set, and Map?
What is the difference between a Stack and a Queue?
Describe a linked list.
What are some common Linux commands? Why are they useful?
What is source control management? Why is it useful?
What are the main states that your files can reside in when using Git?
What are the main sections of a Git project?
What are some common operations you would be performing when using Git?

wk8

What is DCL?
What is TCL?
What is the difference between an aggregate and a scalar function?
What is the GROUP BY clause used for?
What is the ORDER BY clause used for?
What is a stored procedure in SQL?
What is a trigger in SQL?
What is a transaction?
What are the properties of a transaction?
What is a function in SQL?
What is an index in SQL?

What is an algorithm?
How would you describe time complexity?
What is the Factory design pattern?
What is the Singleton design pattern?
What is the difference between linear search and binary search?
What is the difference between Bubble Sort and Merge Sort?

wk9
What is the Optional class?
What is the Stream API and what is it used for?
What is the Reflection API and what is it used for?
What is a thread?
How can we implement multithreading in Java?
What are some states a thread can be in?
What is synchronization?
What is the difference between deadlock and livelock?
Describe the Producer Consumer problem.
What are intermediate stream operations?
What are terminal stream operations?
How can we create a thread?
