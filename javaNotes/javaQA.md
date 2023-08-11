### 1 assign vs declare What is the difference between assigning and declaring a variable?

#### Declare

- syntax:

```java
datatype variableName;
```

- Java is a strongly-typed language which means that all variables in Java must define what type of data we can store into that variable.
- This statement creates a place in memory for Java to store information of that specific datatype.
- camelCase naming convention
- We can refer to this named place in memory using the variable name. If we want to store a value in the variable

#### Assign

- syntax:

```java
variableName = value;
```

- stores a value in the variable
- only work as long as the new variable is of the same datatype

### 2 {} What do a pair of opening and closing curly braces represent?

### 3 source code vs bytecode What is the difference between source code and bytecode?

- Compilation means to transform a program written in a high-level programming language from `source code` into `object code` / `bytecode`.
- `.java` -> `.class`

### 4 method call vs create syntax What is the difference in syntax between calling a method and creating a method?

### 5 What is a method?

> Block of reusable code that can be invoked again and again.

#### `Method Signature`

All methods in a class are defined by:

- their access modifier
- any non-access modifiers
- return type
- method name
- (optionally) a throws exception declaration

Together, these form the `method signature`.

#### Method Parameters

Method parameters are variables passed inside of the parenthesis of the method which we are able to utilize inside of our method. These values are given to us from the entity that invokes the method.

Anytime you can identify repetitive code in your application, abstracting that logic into a method is generally the best solution to keep your program manageable.

```java
int addNums(int n1, int n2) {
  return n1 + n2;
}

// invoking the method
addNums(1, 2);
// storing method return value
// method return value's type = variable type
int total = addNums(1, 2);

```

### 6 What is a variable?

> A `variable` is a container for storing data.

```java
dataType variableName = value;
```

Java is strongly typed meaning that when a variable is declared in Java, the type must be specified.

Types:

- primitive type - data types defined by the language itself
- reference type - data types defined in the Java API or by a programmer

The `variable name` is the unique identifier used to reference that variable again.

### 7 JDK-JRE-JVM What is the difference between the JDK, JRE, and JVM?

`JDK` `Java Development Kit` contains `JRE` and development tools like compiler, debugger, documentation tools.

`JRE` (`Java Runtime Environment`) contains `JVM` and runtime libraries.

`JVM` (`Java Virtual Machine`) runs compiled bytecode in a virtual environment that is same accross every platform. However you need JVM that is specific to the operating system. It uses `JIT` `Just In Time` compiler to turn that bytecode to machine code.

- `JVM` (`Java Virtual Machine`) The JVM is a special program that knows how to execute the programs that you write in Java, Java programs are execute in the JVM. Each operating system has its own JVM.
- `JRE` (`Java Runtime Environment`) contains all the runtime libraries that your code will be calling and using. The JRE contains the JVM within it.
- `JDK` (`Java Development Kit`) provides developer tools like a compiler, debugger, documentation tools, and other command-line utilities. The JDK also has a JRE inside of it

### 8 What is a conditional statement?

`Conditional statement` is a statement that uses a Boolean expressions and only executes the a block of statement if the Boolean expression returns `true`.

- if
- switch
- while
- do-while

### 9 loops Explain the different kinds of loops you can create and use in a program.

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

### 10 Explain the main method.

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
- the array of Strings defined in the method parameters are passed from the command line when the java command is run

### 11 What is a primitive data type? Please list a few and explain them.

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

### 15 How can you iterate over an array?

### 16 What is an array? Why is it useful?

An `array` is a `contiguous block of memory` storing a group of `sequentially stored` elements of the same type.

- fixed size and cannot be resized after declaration
- items in an array are referenced via their index in square bracket notation, which begins with 0 for the first element
- ave a length property specifying the length of the array

```java
// would be filled with the default value of integer: 0
int[] myArray = new int[5];

// OR
int[] otherArray = {1, 2, 3};
```

### 17 What is a stacktrace? How can you use it to debug your application?

> `Stack trace` is a report of the active `stack frames` at a certain point in time during a thread's execution.

Each `JVM thread` (a path of execution) is associated with a stack that's created when the thread is created.

This data structure (stack) is divided into `frames`, which are data structures associated with method calls. For this reason, each thread's stack is often referred to as a method-call stack.

When an exception / error gets thrown. A stack trace is displayed to the console.

### 18 What is the Scanner class used for? Give an example of how you would use it.

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

### 19 if vs switch When would you use an if statement over a switch statement?

- `switch` statement works with:
  - `byte`, `short`, `int`
  - `char`, `String`
  - `enum`
- if the if statement is too long switch can be better

### 20 switch vs if When would you use a switch statement over an if statement?

### 21 What is an operating system?

_Note: You will not be assessed on the different types of operating systems or on process management_

- a software that communicates with the hardware and allows other programs to run
- it is comprised of system software, or the fundamental files your computer needs to boot up and function
- they allow you to install and run programs written for the operating system
- every device (computer, tablet, phone) has an operating system
- the hardware you choose affects what operating system(s) you can run (Windows on PC hardware, Mac OS X Apple, Linux on both)
- they provide

  - Process and `Process Management` (`process` is a program in execution)
  - `Threads` - a thread as a flow of execution through the process code. The thread keeps track of all the instructions that need to be executed next in the program counter. Also, the thread contains system registers that hold the current working variables. Also, the thread's stack contains the execution history.

  - `Scheduling` - in scheduling, the process manager takes the responsibility to remove the running process from the CPU and chooses another process based on a specific strategy.
  - `Memory Management` - the functionality of an operating system that handles and manages the primary memory. Processes move back and forth between the main memory and the disk during the execution.

### 22 full stack What does the term "full stack" mean?

> `Full stack` covers two separate development domains: the front end and the back end.

- The `front end` includes everything that a client, or site viewer, can see and interact with.
- The `back end` refers to all the servers, databases, and other internal architecture that drives the application; usually, the end-user never interacts with this realm directly.
  -Front end platforms are usually built with HTML, CSS, and JavaScript; however, they can also be made via pre-packaged code libraries or content management systems like WordPress.
- Back end developers, in contrast, refine the software code that communicates with servers, databases, or other proprietary software that conveys information to front end interfaces.

### 23 text data type Which datatype represents text in Java?

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

### 24 last array element How would you access the last value in an array if you do not know the size of the array?

### 25 debug crash What steps would you take to debug your program if it crashed with an error message in the console?

### 26 debug wrong result What steps would you take to debug your program if runs, but gives you the wrong results?

### 27 compilation process How would you describe the compilation process for Java?

- 2 steps
  - compiler creates machine independent `bytecode`
  - `JVM` creates machine code

### 28 why methods Give me an example of why you would need to create a method other than the main method.

Calculate triangle area.

### 29 entities of Java Can you describe some of the basic entities of a Java program?

- classes
- variables
- methods

`Classes` are blueprints for creating objects in Java. Classes can have variables and methods within them to represent state and behavior.

`Variables` are containers to store data.

`Methods` are blocks of reusable code.

### 30 benefits of Java What are some of the benefits of Java?

- platform independent,
- has a C-language inspired syntax
- provides automatic memory management
- has an extensive built-in runtime library
- is supported by the Oracle corporation
- has a rich open source community

### 31 What is a flow control statement?

- `if` execute a statement or a block of statements only if some conditional test turns out to be true
- `switch` execute one of several blocks of statements depending on the value of a variable of certain types
- `loops`: allow for the repeated execution of the same statement or block of statements

### 32 What is the modulo operator and why would we use it?

### 33 What is a package and why would we use one?

- a `package` is a collection of classes, interfaces, and enums in a hierarchial manner.
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
- collection of elemnents of the same type
- preserves the order in which elements are inserted
- duplicate entries are allowed. - - - elements are accessed by their index, which begins with 0

List interface includes operations
for the following:

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
- we may want to two instances of _Money_ with same ammount and currancy be the same, in this case we have to change both the `equals()` and `hashCode()` methods

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

### 67-3.16 What is test driven development?

The `TDD` process consists of writing unit tests first, **before** the implemented application code has been written.

`Unit testing` is the testing of individual software components in isolation from the rest of the system.

### 68-3.17 Why are unit tests important?

`Unit testing` is the testing of individual software components in isolation from the rest of the system. This is done by writing unit tests which execute the code we want to inspect.

When developing software, it is important to ensure that most if not all of the code being written is tested to verify the functionality of the code.

One way to ensure this is to follow a process called test-driven development, or TDD.
The TDD process consists of writing unit tests first, before the implemented application code has been written. Then, the implemented application code can be written to make the test pass and the process can be completed for each piece of functionality required.

When refactoring code, the unit tests give us confidence that we can change the source code without breaking existing functionality. This makes debugging much easier.

### 69-3.18 How can JUnit annotations help with running our tests?

`Annotations` are used to support, identify, and execute test method features.

- `@BeforeAll`
- `@BeforeEach`
- `@AfterEach`
- `@AfterAll`
- `@Test`

### 70-3.19 What are the Maven build lifecycle phases?

When Maven builds your project, it goes through several steps called phases

- `validate`: validate the project is correct and all necessary information is available
- `compile`: compile the source code of the project
- `test`: test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
- `package`: take the compiled code and package it in its distributable format, such as a JAR.
- `verify` - run any checks on results of integration tests to ensure quality criteria are met
- `install` - install the package into the local repository, for use as a dependency in other projects locally
- `deploy` - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.

### 71-3.20 Describe the POM.xml file and its importance.

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

### 72-4.1 What is SQL and why would we use this language

`Structured Query Language` (`SQL`) is the language used to administer SQL-based RDBM systems.

### 73-4.2 What are the SQL sublanguages and their purpose?

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

### 74-4.3 What is a RDBMS?

- An RDBMS is a data storage system based on a relational model
- data that is related to a particular object is stored in tables with each entry being represented as a row
- and each data point is a column in the row that is validated by a set of constraints

### 75-4.4 Describe relational database tables.

In MySQL, a table stores and organizes data in columns and rows as defined during table creation.

### 76-4.5 What are constraints and can you describe a few constraints?

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

### 77-4.6 Why would I use the WHERE clause?

FILTERING: The filtering clause of a select statement is a `WHERE` clauses that defines how selected rows are filtered from the table. `WHERE` clauses use logical operators to select records that meet specific conditions.

### 78-4.7 What are some operators that can be used in SQL?

- Arithmetic
- Bitwise
- Comparison
- Compound
- Logical

### 79-4.8 What is the JDBC API and the benefits of using it?

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

### 80-4.9 What is the DAO Design Pattern and why should we use it?

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

### 81-4.10 What information would you need in order to successfully connect to a database?

- URL (`JDBC String`)
- username
- password

## WK 5

### 82-5.1 What is the difference between a Simple and Prepared JDBC statement?

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

### 83-5.2 What is SQL Injection and how can we prevent it using the JDBC?

`SQL Injections` are the exploitation of programming weaknesses in SQL codes to gain access to a database, its resources, and applications.

`PreparedStatement` can be used to prevent SQL injections.

This interface gives us the flexibility of specifying parameters with the ? symbol.

It protects against SQL injection when user input is used by pre-compiling the SQL statement.

### 84-5.3 What is a foreign key?

A `FOREIGN KEY` is a field or collection of fields in a table that refers to the `PRIMARY KEY` of the other table.

- It is responsible for managing the relationship between the tables.
- The table which contains the foreign key is called the `Child Table`, and the table whose primary key is being referred by the foreign key is called the `Parent Table`.

```sql
CREATE TABLE Branch(
    branch_id INT PRIMARY KEY,
    branch_name VARCHAR(20)
     );
-- Add branch_id as foreign key for employee table

ALTER TABLE employee ADD branch_id INT;
ALTER TABLE employee ADD FOREIGN KEY (branch_id) REFERENCES Branch(branch_id);
```

### 85-5.4 What is referential integrity?

`REFERENTIAL INTEGRITY` is the relationship between tables.

Referential Integrity:

- the requirement that a foreign key cannot be defined unless its corresponding primary key exists is a referential integrity constraint
- does not allow the addition of any record in a table that contains the foreign key unless the reference table contains a corresponding primary key.
- does not allow to deletion of a record in a table that contains the foreign key, to delete the record in the parent table, the corresponding record in the child table should be deleted first. to solve this issue `ON DELETE CASCADE` is used.
- Other options are to set the foreign key to null or to its default value (only if the default value references an existing value in the primary-key table).

### 86-5.5 What is normalization?

`Normalization` is the process of organizing the data and the attributes of a database. it is performed to reduce the data redundancy.

### 87-5.6 What is multiplicity?

`Multiplicity` defines the relationship between two tables

- one to one
- one to many
- many to one
- many to many

There are 4 different multiplicity relationships

### 88-5.7 Describe what a join is and explain the different types of joins we can create.

### 89-5.8 What is the difference between a join and a set operation?

### 90-5.9 What is a view and why is it useful?

In `MySQL`, a `View` is a virtual table based on the result-set of an SQL statement. A view consists of rows and columns, just like a common table. The view fields are fields from one or more real tables in the database.

Advantages:

- Structure data in a way that users or classes of users find natural or intuitive.
- Restrict access to the data in such a way that a user can see and manipulate exactly what they need.
- Summarize data from various tables which can be used to generate documents and reports.

```sql
CREATE VIEW view_name AS SELECT column1, column2, ... FROM table_name WHERE condition;
```

### 91-5.10 What is HTTP? Why is it important to know about?

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

### 92-5.11 What are common HTTP verbs used when a client application is making a request?

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

### 93-5.12 What are some common HTTP status codes that can be included in a response?

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
