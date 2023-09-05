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
