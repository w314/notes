## Optionals

_Know using Optional.of(), Optional.empty(), Optional.ofNullable(), and isPresent() and get(), orElse()_
_Everything else is supplementary_

> What is the Optional class?

It is a container object used to hold a value which could be non-null or null, and provides easy ways of handling either case

- The purpose of the class is to provide a type-level solution for representing optional values instead of null references.

- To overcome frequent occurrences of NullPointerException, Java 8 has introduced a new class Optional in java.util package.
- By using Optional, we can specify alternate values to return or alternate code to run.

- do not use Optionals as method parameters
- The intent of Java when releasing Optional was to use it as a return type, thus indicating that a method could return an empty value
- using Optional in a serializable class will result in a `NotSerializableException`

### Creating Optional Objects

#### `Optional.empty()`

Create empty Optional object with the Optional's class `.empty()` static method:

```java
// creating empty optional object
Optional<String> myEmptyObject = Optional.empty();
```

- static method

#### `Optional.of()`

Create an Optiona object with a value, using `.of()`:

```java
// creating optional/ object with a value
String myString = "value";
Option<String> objectWithValue = Optional.of(myString);
```

- static method
- argument passed to `.of()` cannot be null
- otherwise, we'll get a `NullPointerException`

#### `Optional.ofNullable()`

For values that may be null.

```java
String myString = null;
Optional<String> myMaybeEmptyObject = Optional.ofNullable(myString);
```

- static method
- won't throw an exception
- in case of null value passed, returns an empty Optional object

#### Checking if value is present

##### `.isPresent()`

When we have an `Optional` object returned from a method or created by us, we can check if there is a value in it or not with the `.isPresent()` method:

```java
opt = Optional.ofNullable(null);
boolean optHasValue = opt.isPresent();
```

- return true if the wrapped value is not null

##### `.isEmpty()`

```java
opt = Optional.ofNullable(null);
boolean optHasValue = opt.isEmpty();
```

- as of Java 11

##### `.ifPresent()`

```java
// instead of old-school
if(name != null) {
    System.out.println(name.length());
}

// NOW BEST PRACTICE
Optional<String> opt = Optional.of("bobek");
opt.ifPresent(name -> System.out.println(name.length()));
```

### Retrieve value form Optional object

#### `.orElse()`

The orElse() method returns the wrapped value if it's present, and its argument otherwise:

```java
String nullName = null;
String name = Optional.ofNullable(nullName).orElse("john");
```

#### `.get()`

`.get()` can only return a value if the wrapped object is not null; otherwise, it throws a `NoSuchElementException`:

```java
Optional<String> opt = Optional.of("baeldung");
String name = opt.get();
```

Therefore, this approach works against the objectives of Optional and will probably be deprecated in a future release.

## Reflection API

_How to use Class class and related classes in reflect package to find and work with class members_

> What is the Reflection API and what is it used for?
> Reflection is a feature in the Java programming language. It allows an executing Java program to examine or "introspect" upon itself, and manipulate internal properties of the program. For example, it's possible for a Java class to obtain the names of all its members and display them.

- The ability to examine and manipulate a Java class from within itself simply doesn't exist in other programming languages
- One tangible use of reflection is in JavaBeans, where software components can be manipulated visually via a builder tool. The tool uses reflection to obtain the properties of Java components (classes) as they are dynamically loaded.

### Steps to use Reflection

The reflection classes, such as Method, are found in `java.lang.reflect`. There are three steps that must be followed to use these classes.:

##### 1. obtain a java.lang.Class object for the class that you want to manipulate

- java.lang.Class is used to represent classes and interfaces in a running Java program.
  Retrieve references to classes with:
- `Object.getClass()` method
- `obj.class`
- `Class.forName()` method

##### 2. call a method

Call a method such as getDeclaredMethods to get a list of all the methods declared by the class.

##### 3. use the reflection API to manipulate the information

##### Example:

To display a textual representation of the first method declared in String:

```java
// 1. obtain class object
Class c = Class.forName("java.lang.String");
// 2. call method
Method m[] = c.getDeclaredMethods();
// 3. manipulate information
System.out.println(m[0].toString());
```

### Reflection API Usage

#### Get Information About Class

- `.isInstance()`
- `.getDeclaredMethods()`
- `.getDeclaredConstructors()`
- `.getDeclaredFields()`

#### Invoke a method by name

#### Change values of fields

#### Creating and manipulating arrays

## Stream API

> What is the Stream API and what is it used for?

The Stream API is a functional-style way of defining operations on a stream of elements.

- Streams are an abstraction which allow defining operations which do not modify the source data and are lazily executed.
- Streams do not store data, they simply define operations like filtering, mapping, or reducing, and can be combined with other operations and then executed.
- Some built-in Streams are located in the java.util.stream package.
- Streams are divided into intermediate and terminal operations.
  - Intermediate streams return a new stream and are always lazy - they don't actually execute until a terminal operation is called.
  - Terminal operations trigger the execution of the stream pipeline, which allows efficiency by perfoming all operations in a single pass over the data.
- Finally, reduction operations take a sequence of elements and combine them into a single result.
  - Stream classes have the reduce() and collect() methods for this purpose, with many built-in operations defined in the Collectors class.

### terminal vs intermediate operations

In the Java Stream API, intermediate operations are operations which are lazily executed and return another Stream and terminal operations are operations which initiate the execution when invoked .

> What are intermediate stream operations?

> What are terminal stream operations?

### reduction operations

### common terminal operations

- collect()
- reduce()
- forEach()

### common intermediate operations

- filter()
- map()
- sorted()

### Example

```java
//Filter
public void streamFilter(List<Associate> associateList, String filter) {
  //Filter receives a Predicate<T> as parameter
  associateList.stream().filter((Associate a) -> new StringBuilder(a.getFirstName()).indexOf(filter) != -1)
  .forEach((Associate a) -> { System.out.println(a.getFirstName()); });
}

//Max
public int streamMax(int[] array) throws IllegalArgumentException {
  if(array == null) {
    logger.warn("User sent null array.");
    throw new IllegalArgumentException("Can't process a null array.");
  }
  return Arrays.stream(array).max().getAsInt();
}


public static void main(String[] args) {
		Stream stream = new Stream();

		List<Associate> associateList = new ArrayList<>();

    /** Filter **/
		String filter = "r";
		System.out.println("Iterating over list with filter(" + filter + ")");
		stream.streamFilter(associateList, filter);
}

```

## Multithreading

> What is a thread?

A thread is a subset of a process that is also an independent sequence of execution, but threads of the main process run in the same memory space, managed independently by a scheduler. So, we can think of a thread as a "path of execution", but they can access the same objects in memory.

Every thread that is created in a program is given its own call stack, where it stores local variables references. However, all threads share the same heap, where the objects live in memory. Thus, two threads could have separate variable references on two different stacks that still point to the same object in the heap.

### Concurrency

`Concurrency` refers to breaking up a task or piece of computation into different parts that can be executed independently, out of order, or in partial order without affecting the final outcome.

- One way - but not the only way - of achieving concurrency is by using multiple threads in the same program.
- Operating systems use concurrency to manage the many different programs that run on them.

### Multi-core Processing

Most computers these days have multiple cores or CPUs, which means that calculations at the hardware level can be done in parallel.

- On multi-core systems, different processes can be run on different CPUs entirely. This enables true parallelization and is a key benefit of writing multithreaded programs.
- Without multiple cores, operating systems can still achieve concurrency with a process called `time splicing` - this means running one process for a short time, then switching to another, and back very rapidly. This ensures that no process or application is completely blocked.

#### Real World Application of MultiThreading

- a browser that starts rendering a web page while it is still downloading the rest of page.
- Airplane ticket reservation system where multiple customers accessing the server.
- Multiple bank account holders accessing their accounts simultaneously on the bankSA server.

### Multithreading in Java

In Java, multithreading is achieved via the `Thread class` and/or the `Runnable interface`.

In general, it is best to avoid implementing multithreading yourself if possible.

- The benefit of multithreaded applications is better performance due to non-blocking execution.
- However, you should always measure or attempt to estimate the performance benefit you will get by using threads versus the tradeoff in complexity and subtle bugs that might be generated.
- Usually there are frameworks, tools, or libraries that have implemented the problem you are trying to solve, and you can leverage those instead of trying to build your own solution.

#### Thread Class

##### important methods:

- getters and setters for:
  - id
  - name
  - priority
- `interrupt()` - to explicitly interrupt the thread
- to test the state of the thread:
  - `isAlive()`
  - `isInterrupted()`
  - `isDaemon()`
- `join()` - to wait for the thread to finish execution
- `start()` - to begin thread execution after instantiation

##### important static methods:

- `Thread.currentThread()` - returns the thread that is currently executing
- `Thread.sleep(long millis)` - causes the currently executing thread to temporarily stop for a specified number of milliseconds

##### Thread Priorities

Priorities signify which order threads are to be run. The Thread class contains a few static variables for priority:

- MIN_PRIORITY = 1
- NORM_PRIORITY = 5, default
- MAX_PRIORITY = 10

##### Creating Threads using Thread class

> How can we create a thread?

- create a class that `extends Thread`
- implement the `run()` method
- instantiate your class
- call the `start()` method

```java
// create a class that extends Thread
public class MyThread extends Thread {
  // implement the run() method
  @Override
  public void run() {
    System.out.println("Inside the MyThread class");
  }
}

public class ThreadDemo {
  public static void main(String[] args) {
    // instantiate your class
    Thread myThread = new MyThread();
    // call the `start()` method
    myThread.start();
  }
}
```

> How can we implement multithreading in Java?

### Runnable interface

`java.lang.Runnable` is an interface that is to be implemented by a class whose instances are intended to be executed by a thread.

To create a class that implements the Runnable functional interface

- implement the run() method
- pass an instance of your class to a Thread constructor
- call the start() method on the thread

Because Runnable is a functional interface, we can use a lambda expression to define thread behavior inline instead of implementing the interface in a separate class.
We pass a lambda expression as the Runnable type required in the Thread constructor.

### important class members

### Thread states

> What are some states a thread can be in?

## Synchronization

_Know the following concepts at a high level:_

- Deadlock
- Livelock
- Producer-Consumer Problem

> What is synchronization?

> What is the difference between deadlock and livelock?

### Producer-Consumer Problem

> Producer-Consumer Problem
