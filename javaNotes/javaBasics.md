## Java Programming Language

> Java What are some of the benefits of Java?

### Features of Java

- strongly typed
- general purpose
- provides automatic memory management
- platform independent
- object oriented
- has a C-language inspired syntax

### Benefits of Java

- has an extensive built-in runtime library
- is supported by the Oracle corporation
- popular, has a rich open source community

## Garbage Collection

Garbage collection is a background process created by JVM to delete unused objects from the heap

> What is the role of garbage collection in Java?

- deletes objects which have no references to them
- calls `.final()` method of objects
- frees up space for us
- we don't control the garbage collector, there is no way we can explicitly force garbage collection to happen, but we can request garbage collection to be run through the use of one of the following:
  - System.gc()
  - Runtime.getRuntime().gc()
  - System.runFinalize()

## Debugging

> What is a stacktrace? How can you use it to debug your application?

`Stack trace` is a report of the active `stack frames` at a certain point in time during a thread's execution.
- Each `JVM thread` (a path of execution) is associated with a stack that's created when the thread is created.
`Stack frame` is a data structure associated wiht method calls. Each method call gets its own stack frame in the stack.


This data structure (stack) is divided into `frames`, which are data structures associated with method calls. For this reason, each thread's stack is often referred to as a method-call stack.

When an exception / error gets thrown. A stack trace is displayed to the console.

### Reading Stacktraces

- contain the type of issue encountered
- may contain a useful message
- record method call chain
- record line numbers + files

> What steps would you take to debug your program if it crashed with an error message in the console?

> What steps would you take to debug your program if runs, but gives you the wrong results?

> If there was an error in the console when you tried to run your program, how would you debug?

## General Program execution
- What does System.exit(0) do?
System.exit(0) in Java terminates the currently running Java virtual machine (JVM). The argument 0 indicates a successful termination. Generally, a non-zero argument (e.g., System.exit(1)) indicates an abnormal termination due to an error or other issue. The argument passed to System.exit() is typically used as an exit code that can be queried by the operating system or calling process.



## Errors & Exceptions

> What is the difference between an Error and an Exception?

Both `Error` and `Exception` extend the `Throwable` class

### `Error`

- `Compilation Error`

  - occurs at compile time
  - syntax error
  - not handling checked exceptions
  - eg: `SyntaxError`

- `Runtime Error`

  - occurs at runtime
  - severe problem with the program
  - we dot hand attempt to recover from them
  - eg: `OutOfMemoryError`

### `Exception`

Exceptions are the conditions that occur at runtime and may cause the termination of the program. But they are recoverable using try, catch and throw keywords.

#### Exception Handling

> How would you handle an exception?

Exception can be recovered from with `try - catch`:

- checked
  - must be handled
  - eg: `IOException`
- unchecked
  - runtime errors
  - eg: `ArrayOutOfBounds`

When risky code is written that has the possibility of throwing an exception, it can be dealt with in one of two ways:

1. `Handling` means that the risky code is placed inside a `try/catch` block
2. `Declaring` means that the type of exception to be thrown is listed in the method signature with the throws keyword. This is also called "ducking" the exception - you let the code which calls the method deal with it.

If the exception is not handled anywhere in the program, it will propagate up through the call stack until it is handled by the JVM which then terminates the program.

> What is the difference between a checked and an unchecked exception?

- Checked exception require mandatory handling:

  - try - catch
  - throws

- Handling the exception is checked during compilation, gives compliation error if not handled.

- Exception-handling is mandatory for any exception class that is not a subclass of either Error or RuntimeException.

#### Creating Custom Exceptions

- A programmer can create custom exceptions in Java by extending any exception class.
- If you extend RuntimeException, however, you will be creating an unchecked exception.
  - This is a good idea if you do not want other code to have to handle your exception being thrown.
  - If you do always want to require your exception to be handled, then create a checked exception by extending any existing one, or the Exception class itself.

## Java Entities

> Can you describe some of the basic entities of a Java program?

- `classes` - blueprints for creating objects,  can have variables and methods within them to represent state and behavior
- `variables` - containers to store data
- `methods` - blocks of reusable code

### Java Methods

> What is a method?

A `method` is a block of reusable code that can be invoked again and again.

> What is the difference in syntax between calling a method and creating a method?

#### `Method Signature`

All methods in a class are defined by:

- their access modifier
- any non-access modifiers
- return type
- method name
- parameters
- (optionally) a throws exception declaration

Together, these form the `method signature`.

#### `Method Parameters`

- Method parameters are variables passed inside of the parenthesis of the method which we are able to utilize inside of our method. These values are given to us from the entity that invokes the method.

```java
// METHOD CREATION SYNTAX
int addNums(int n1,

 int n2) {
  return n1 + n2;
}

// METHOD CALL SYNTAX
addNums(1, 2);
// storing method return value
// method return value's type = variable type
int total = addNums(1, 2);

```

### Scope

Part of the program where a variable of method exits.

When a variable or method is declared in a Java program, its0 scope determines where the variable or method exits.

> What are the different scopes in Java?

- `Instance, or object scope` - The variable is attached to individual objects created from the class.
- `Class, or static scope` - Resides on the class definition itself.
- `Method scope` - Declared within a method block; only available within the method in which they are declared.
- `Block scope` - Only exist within the specific control flow block (for, while, etc.)

> If I define a variable within a method, how can I access its value outside of the method?

### Classes

Class members:

- variables
- methods
- constructors

(Variables and methods that are NOT static are instance members.)

#### Access Modifiers

> What are the four levels of access we can give to class members? How are they different from one another?

`Access Modifiers` set access level of methods, variables, classes and constructors

- `public`: can be accessed by any classes
- `default` (when there is no access modifier): within the same package only
- `protected`: within package + outside of package through inheritance
- `private`: only within the class, a class (except a nested class) cannot be private

#### Abstract Class

An `abstract` class is a class that is declared abstract —it may or may not include abstract methods.

- Abstract classes cannot be instantiated, but they can be subclassed.
- An abstract class can have 0 or more abstract methods, but if a class has at least one abstract method then the whole class has to be abstract.
- An abstract class can have implemented methods as well.
- Use the extends keyword to extend an abstract class.

> What is the difference between using an instance variable and a static variable?

## Java Programs

### Package

> What is a package and why would we use one?

`Package` is a collection of classes, interfaces, and enums in a hierarchical manner.

- folders for organizing files
- also a way to manage accessibility

#### Benefits of Package

- keep your classes separate from the classes in the Java API
- reuse classes in other applications.
- distribute your classes to others.

#### Syntax

- for source files within a package, they need a **package declaration**

  - declare package in the first (non-commented) line in a .java file
  - declares the package in which the class will reside
  - use reverse domain name : lowercase characters separated by periods in the reverse way you would specify a web domain (com.revature.mypackage)

  <br>

- to use functionality from another package, you'll need an **import statement**
  - by default, everything in the `java.lang` package is imported.

<br>

```java
// declare the package this class belongs to
package com.revature.mypackage;

// import other packages to use
import java.util.*;
```

### Main method

> Explain the main method.

```java
public class HelloWorld{
  public static void main(String[] args) {
    System.out.println("Hello, World!");
  }
}
```

- `public` is an access modifier
- `static` is a non-access modifier sets the scope
- `void` is the "return type" of the method
- `String[] args` array of Strings defined in the method parameters are passed from the command line when the java command is run

### Flow Control

- structures that make the execution of the program non-linear
- 2 types
  - Conditional Statements
  - Loops

#### Java Conditional Statements

> What is a conditional statement?

`Conditional statement` is a statement that uses a Boolean expressions and only executes the a block of statement if the Boolean expression returns `true`.

- flow control statement
- code block that may execute depending on a condition
- usually there are multiple "branches" - one of which may execute
- examples:
  - `if` statements
  - `switch` statements

##### If Statements

`if` - execute a statement or a block of statements only if some conditional test turns out to be true

##### Switch Statements

`switch` - execute one of several blocks of statements depending on the value of a variable of certain types

> When would you use an if statement over a switch statement?

- `switch` statement works with:
  - `byte`, `short`, `int`
  - `char`, `String`
  - `enum`
- if the if statement is too long switch can be better

#### Java Loops

`Loops` are java statements that allow for the repeated execution of the same statement or block of statements.

> Explain the different kinds of loops you can create and use in a program.

- flow control statments.
- code block that may execute and repeat depending on a condition
- examples:
  - `for`
  - `while`
  - `do-while`

##### For Loop

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
```

##### While Loop

```java
// WHILE loop
int i = 0;
while (i < 3) {
  System.out.println(i);
  i++;
}
```

##### Do-While Loop

```java
// DO WHILE loop
int i = 4;
do {
  System.out.println(i);
} while(i < 3);

```

## Object Class

`Object` is a special class in Java which is the root class from which all other classes inherit, either directly or indirectly.

### Object Class Methods

- Object `.clone()` - Returns a copy of this object.
- boolean equals(Object o) - Indicates whether this object is equal to the o object.
- void finalize() - Called by the garbage collector when the object is destroyed.
- Class<?> getClass() Returns a Class object that represents this object's runtime class
- int hashCode() - Returns this object's hash code.
- void notify() - Is used with threaded applications to wake up a thread that's waiting on this object.
- void notifyAll() - Is used with threaded applications to wake up all threads that are waiting on this object.
- String toString() - Returns a String representation of this object.
- void wait() - Causes this object's thread to wait until another thread calls notify or notifyAll.
  - void wait(long timeout) - Is a variation of the basic wait method.
  - void wait(long timeout, int nanos) - Another variation of the wait method.

> What methods are commonly overridden from the Object class and why?

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



### abstract class vs. interface
- interface CANNOT have implementations to its method
- unless you use `default`
- you use `extends` to extend classes
- you use `implements` with interfaces

> See Java String

> See Java Arrays



CHecked Exception
- compile time

Unchecked
- runtime exception


How ot compare two objects

obj1.equals(obj2) but has to have equals override


public satic...
access modifier, scope, return type, method name, parameter type, and parameter name

Singleton
example: Beans are singletons by default



Collections
know see

arrays are statically sized
arrayList are dinmaically sized

Collection only take objects
arrays can take primitives

Collection API
list set and queue interfaces


linkedlist implemetn list and queue

hashtable vs hashmap?

- Synchronization
  - HashTable is synchronized (threadsafe) and can be shared between multiple threads
- Null keys and null values
  - HashTable does not allow null keys or null values
  - HashMap allows one null key and any number or null values
- Iteration
  -  HashMap iterator is fail-fast, will throw a `ConcurrentModificationException` if the map is structurally modified while iterating over it
  - HashTable does not do that
- Performance
  - HashMap is faster and uses less memory 
  - as HashMap is unsynchronized
- Legacy
  - HashTable is legacy class
  - HashMap is part of newer Collections Framework


Optional 

avoid nullpointerexception have safer code



