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

## Stack & Heap

> Describe the difference between the stack and the heap.

JVM divides memory into stack and heap memory.

### `Stack`

- area in memory
- keeps track of the currently executing methods
- stores any variables that these methods create and use
- smaller than heap
- `Stack` Memory in Java is used for:
  - static memory allocation
  - the execution of a thread.
  - it contains:
    - primitive values that are specific to a method
    - references to objects referred from the method that are in a heap.
- LIFO : Access to this memory is in Last-In-First-Out (LIFO) order.
- When the method finishes execution, its corresponding stack frame is flushed, the flow goes back to the calling method, and space becomes available for the next method.
- It grows and shrinks as new methods are called and returned, respectively.
- Variables inside the stack exist only as long as the method that created them is running.
- It's automatically allocated and deallocated when the method finishes execution.
- If this memory is full, Java throws `java.lang.StackOverFlowError`.
- Access to this memory is fast when compared to heap memory.
- This memory is `threadsafe`, as each thread operates in its own stack.

### `HEAP`

- used for the dynamic memory allocation of Java objects and JRE classes at runtime.

#### String Pool

- special are in Heap to store String objects
- a String is stored in Sting Pool if object was created using **literal notation** (double quotes)
- a String is stored outside of pool if object was created using **object notation** (new keyword + constructor) EVEN IF object is already in the pool

### `Stack` vs `Heap`

- static vs dynamic memory allocation
- fast vs. slow memory access
- `java.lang.StackOverFlowError` vs `java.lang.OutOfMemoryError`
- automatic memory flush vs garbage collection
- threadsafe vs not threadsafe

<table>
<thead>
<tr>
<td><strong>Parameter</strong></td>
<td><strong>Stack Memory</strong></td>	<td><strong>Heap Space</strong></td></tr>
</thead>
<tbody>
<tr>
<td><strong>Application</strong></td>
<td>Stack is used in parts, one at a time during execution of a thread</td>
<td>The entire application uses Heap space during runtime</td>
</tr>
<tr>
<td><strong>Size</strong></td>
<td>Stack has size limits depending upon OS, and is usually smaller than Heap</td>
<td>There is no size limit on Heap</td>
</tr>
<tr>
<td><strong>Storage</strong></td>
<td>Stores only primitive variables and references to objects that are created in Heap Space</td>
<td>All the newly created objects are stored here</td>
</tr>
<tr>
<td><strong>Order</strong></td>
<td>It's accessed using Last-in First-out (LIFO) memory allocation system</td>
<td>This memory is accessed via complex memory management techniques that include Young Generation, Old or Tenured Generation, and Permanent Generation.</td>
</tr>
<tr>
<td><strong>Life</strong></td>
<td>Stack memory only exists as long as the current method is running</td>
<td>Heap space exists as long as the application runs</td>
</tr>
<tr>
<td><strong>Efficiency</strong></td>
<td>Much faster to allocate when compared to heap</td>
<td>Slower to allocate when compared to stack</td>
</tr>
<tr>
<td><strong>Allocation/Deallocation</strong></td>
<td>This Memory is automatically allocated and deallocated when a method is called and returned, respectively</td>
<td>Heap space is allocated when new objects are created and deallocated by Garbage Collector when they're no longer referenced</td>
</tr>
</tbody>

</table>

## Garbage Collection

Garbage collection is a background process created by JVM to delete unused objects from the heap

> What is the role of garbage collection in Java?

- deletes objects which have no references to them
- call objects `.final()` method
- frees up space for us
- we don't control the garbage collector, there is no way we can explicitly force garbage collection to happen, but we can request garbage collection to be run through the use of one of the following:
  - System.gc()
  - Runtime.getRuntime().gc()
  - System.runFinalize()

## Debugging

> What is a stacktrace? How can you use it to debug your application?

`Stack trace` is a report of the active `stack frames` at a certain point in time during a thread's execution.

Each `JVM thread` (a path of execution) is associated with a stack that's created when the thread is created.

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

## Errors & Exceptions

> What is the difference between an Error and an Exception?

Both `Error` and `Exception` extend the `Throwable` class

### `Error`

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

### `Exception`

Exceptions are the conditions that occur at runtime and may cause the termination of the program. But they are recoverable using try, catch and throw keywords.

#### Exception Handling

> How would you handle an exception?

Exception can be recovered from with `try - catch`:

- two types
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

- classes
- variables
- methods

`Classes` are blueprints for creating objects in Java. Classes can have variables and methods within them to represent state and behavior.

`Variables` are containers to store data.

`Methods` are blocks of reusable code.

### Java Variables

> What is a variable?

A `variable` is a container for storing data.

#### Variable Types

- `primitive data type` - data types defined by the language itself
  - the type of a primitive variable determines the range of values that a primitive variable can store
  - stored in the stack
- `reference data type` - data types defined in the Java API or by a programmer
  - stores the reference to an object in memory
  - the type of a reference variable determines what types of objects a reference variable can store a reference to

> What is a primitive data type? Please list a few and explain them.

- data types defined by the language
- stores the value of the data
- types
  - boolean - `true` or `false`
    - `boolean` - 1 bit
  - character - uses `''`
    - `char` - 2 bytes
  - numerical
    - `byte` - 1 byte
    - `short` - 2 bytes
    - `int` - 4 bytes
    - `long` - 8 bytes
  - floating points
    - `float` - 4 bytes
    - `double` - 8 bytes

#### Using variables

```java
dataType variableName = value;
```

> What is the difference between assigning and declaring a variable?

##### Declaring a variable

```java
datatype variableName;
```

- The `variable name` is the unique identifier used to reference that variable again
- Java is a strongly-typed language which means that all variables in Java must define what type of data we can store into that variable.
- This statement creates a place in memory for Java to store information of that specific datatype.
- camelCase naming convention

##### Assigning value to a variable

If we want to store a value in the variable:

```java
variableName = value;
```

- stores a value in the variable
- only work as long as the new variable is of the same datatype

#### Opearators

- special symbols that perform a task
- use one or more operands, or values
- have precedence, just like math

#### Operator Categories

- arithmetic
- assignment
- comparison
- logical

> What is the modulo operator? How is it useful?

#### Assignment Operators

> What are shorthand assignment operators?

Assignment operators assign value to a variable.

= += -= \*= /= %= &= ^=

> How do you use increment and decrement operators?

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

#### Casting

> What is explicit and implicit casting?

`Casting` is the process of converting a data type to another data type.

`implicit casting`

- AKA widening or upcasting
- automatically done by Java
- does it with primitive data types
- where there is no loss of data

  - If one of the values is a double, the other value is converted to a double
  - If neither is a double but one is a float, the other is converted to a float.
  - If neither is a double nor a float but one is a long, the other is converted to a long.
  - If all else fails, both values are converted to int.

`explicit casting`

- AKA narrowing or downcasting
- done by programmer
- uses `()`:

```java
int i = 200;
short s = (short)i;
```

- In some cases you will have to use the data type's own methods to convert. Some of these methods are listed in the table below.
  - `String` to `int` with `Integer.parseInt(String)`
  - `int` to `String` with `String.valueOf(int)`

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

When a variable or method is declared in a Java program, it is attached to a specific scope within the program, which determines where the variable or method exits.

> What are the different scopes in Java?

- `Instance, or object scope` - The variable is attached to individual objects created from the class.
- `Class, or static scope` - Resides on the class definition itself.
- `Method scope` - Declared within a method block; only available within the method in which they are declared.
- `Block scope` - Only exist within the specific control flow block (for, while, etc.)

> If I define a variable within a method, how can I access its value outside of the method?

#### Static Keyword

The static keyword in Java is mainly used for memory management. The static keyword in Java is used to share the same variable or method of a given class.

When a member is declared static, it can be accessed before any objects of its class are created, and without reference to any object.

A static variable is a variable of a class that isn’t associated with an instance of a class.

Instead, the variable belongs to the class itself.

As a result, you can access the static variable without first creating a class instance.

> What is the difference between calling an instance method and a static method?

A static method is a method of a class that isn’t associated with an instance of a class.

Instead, the method belongs to the class itself.

As a result, you can access the static method without first creating a class instance.

##### How to use Static members

- within same class: just use name of member
- in another class: use class name and then name of member using dot notation
- example:
  - Math.min(4, 5)
  - Math.PI

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

##### Interfaces

An `interface` is similar to an abstract class, but one of many differences is that a class can only inherit one other class, but a class can implement as many interfaces as it needs.

> Why would you use an interface over an abstract class?

- A class implements an interface using the `implements` keyword in the class definition and by providing implementations for any abstract methods defined by the interface.
- Interfaces have these advantages over class:
  - Implementation details do not need to be provided in the interface.
  - A class can only extend one other class, but it can implement as many interfaces as needed.
- Interfaces have `implicit modifiers` on methods and variables.
  - **Methods** are '`public`' and '`abstract`'
  - **Variables** are '`public`', '`static`', and '`final`'

#### Wrapper Classes

- every primitive has a corresponding object type
- mainly useful when working with Collections

##### Autoboxing

> What is autoboxing and unboxing?

- `Boxing` - the process of converting a primitive to its wrapper clas
- `Unboxing` is the reverse - converting a wrapper class to its primitive.
- `autoboxing` - a feature in which both boxing and unboxing done implicitly by Java. Example: when passing an `int` variable as parameter to a function requesting an `Integer`
- Wrapper classes have static helper methods like .parseX() and .valueOf() for explicit primitive conversion.

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
- `static` is a non-access modifier
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

### Input - Output

#### Scanner class

> What is the Scanner class used for? Give an example of how you would use it.

The `Scanner` class is used to get user input.

- found in the `java.util` package

```java
import java.util.Scanner;

class Main {
  public static void main(String[] args) {
    // create Scanner object
    Scanner myScanner = new Scanner(System.in);

    // prompt user for input
    System.out.println("Enter username:");

    // read and store user input
    int userAge = myScanner.nextInt();
    // consume hidden newLine character
    myScanner.nextLine();

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
- `nextLine()`
  - Reads a String value from the user
  - OR used to consume hidden newline character (between calling two nextInt() for example)
- `nextLong()` Reads a long value from the user
- `nextShort()` Reads a short value from the user

If you enter wrong input (e.g. text in a numerical input), you will get an exception/error message (like `InputMismatchException`).

#### Print Statements

## Object Class

`Object` is a special class in Java which is the root class from which all other classes inherit, either directly or indirectly.

### Object Class Methods

- Object clone() - Returns a copy of this object.
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

## String Class

> Which datatype represents text in Java?

Strings.

- use ""
- are not a primitive data type but a reference type
- holds a reference to an object created from the String class, not the value of the string itself
- Strings are `immutable`, constant objectsm, this is accomplished by having internal, private and final fields and not implementing any "setter" methods which would alter the state of those fields.
- Because Strings are immutable, all of the methods in the String class return a new String - the original is not modified.
- When Strings are created they are placed in a special location within the `heap` called the `String Pool`.
- When String literals are created, if there is an existing String that matches in the String Pool, the reference variable will point to the existing value.
- Duplicates will not exist in the String Pool. This is important because Strings take up a lot of memory. Being able to reuse the same value throughout your application is advantageous.
- One way to circumvent the above process is to use the new keyword along with the String constructor, which will explicitly create a new String object in memory, even if one already exists in the String Pool.

### String methods:

- `toUpperCase()` -Converts all the characters of a string to upper case.
- `toLowerCase()`-Converts all the characters of a string to lower case
- `charAt(int index)` -This returns the indexed character of a string, where the index of the initial character is 0
- `concat(String s)` -This returns a new string consisting which has the old string + s
- `equals(String s)` -Checks if two strings are equal
- `equalsIgnoreCase(String s)` -This is like equals(), but it ignores the case(Ex: ‘Hello’ and ‘hello’ are equal)
- `length( )` -Returns the number of characters in the current string.
- `replace(char old, char new)` -This returns a new string, generated by replacing every occurrence of old with new.
- `trim()` -Returns the string that results from removing white space characters from the beginning and ending of the current string.
- `.substring(int beginningInd, int endIndex)` - end index is optional
- `.toCharArray()` - converts String to `char[]` array

### Working with Strings

- String to Integer

```java
int x = Integer.parseInt("1234");
```

- String to Array

```java
String words = "once upon";
String[] wordArray = words.split(" ");
```

> If you received text input from the user, how would you go about comparing it to a value, like "yes" or "no"?

```java
String str1 = "yes";
String str2 = "no";
boolean isSame = str1.equals(str2);
```

## Java Arrays

> What is an array? Why is it useful?

An `array` is a `contiguous block of memory` storing a group of `sequentially stored` elements of the same type. Provies fast data access.

- fixed size and cannot be resized after declaration
- indexed - items in an array are referenced via their index in square bracket notation, which begins with 0 for the first element
- have a length property specifying the length of the array
- can be iterated over

```java
int[] myArray = new int[5];
// OR
int[] otherArray = {1, 2, 3};
```

> How can you iterate over an array?

> How would you access the last value in an array if you do not know the size of the array?

#### Array Static Methods

- `Arrays.sort()`
- `Aarrays.binarySearch()` - array must be sorted
- `Arrays.toString()`
- `Arrays.equals(array1, array2)` - compares the contents of the arrays

```java
// create a new array
int[] myArray = new int[5];
// OR
int[] myArray1 = {2, 6, 7};

// lenght of the array
myArray.length;

// print out array
System.out.println(Arrays.toString(myArray));


```

> What is the difference between an array and an ArrayList?
