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

`polymorphism` means "taking on many forms". In the realm of programming, it describes how objects can behave differently in different contexts. In OOP polymorphism provides the means to perform a single action in multiple different ways

The most common examples of polymorphism:

- `method overloading`: when there are two or more methods in a class with the same method name, but different method signatures by changing the parameter list.
  - change in number of parameters
  - change in types of parameters
  - compile time / static polymorphism
- `method overriding`: when a method in a child class has the same method signature as a method in the parent class, but with a different implementation

  - make class hierarchies more flexible and dynamic
  - runtime / dynamic polymorphism
  - `static methods` cannot be overriden
  - return type can only be changed if it is a subtype of the original type (`covariant return types`)
  - access modifier can be changed but must provide more _not less_ access

  `virtual method invocation` when variable is declared as type Animal but refers to a Dog object, calling the method spead will use Dog's implementation of the method

- `upcasting`: is the process of casting an object of a subclass to an object of its superclass
  - done automatically by the Java compiler
  - safe operation does not involve loss of data
  - you can access only the members of the superclass, but don not lose any members of the subclass
- `downcasting`: the process of casting an object of a superclass to an object of its subclass
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
  `Interface Segregation Principle (ISP)`: Clients should not be forced to depend on interfaces they do not use, emphasizing specific interfaces tailored to clients' needs and reducing unnecessary dependencies.
- `Dependency Inversion Principle (DIP)`: High-level modules should not depend on low-level modules; both should depend on abstractions, promoting loose coupling and dependency inversion through abstractions.

### 3.13 What is Maven? Why would we use it?

`Maven` is a tool that can be used for building and managing any Java-based project.

- A build automation and dependency management tool for Java. Maven project configuration and dependencies are handled via the `Project Object Model`, defined in the `pom.xml` file.
- A testing framework
- A logging library which allows for multiple logging thresholds
- A library of tools for adding functionality to a Java application

### 3.14 What is the SDLC? Why is it important?

### 3.15 When would you use an Agile methodology versus Waterfall?

### 3.16 What is test driven development?

### 3.17 Why are unit tests important?

### 3.18 How can JUnit annotations help with running our tests?

### 3.19 What are the Maven build lifecycle phases?

### 3.20 Describe the POM.xml file and its importance.
