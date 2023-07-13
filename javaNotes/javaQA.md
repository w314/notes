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