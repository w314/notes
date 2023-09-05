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

Multithreading extends the idea of multitasking into applications where you can subdivide operations in a single application into individual, parallel threads.

- Each thread can have its own task that it performs.
- The OS divides processing time not just with applications, but between threads.
- Multi-core processors can actually run multiple different processes and threads concurrently, enabling true parallelization.
- In Java, multithreading is achieved via the `Thread class` and/or the `Runnable interface`.

> What is a thread?

A thread is a subset of a process that is also an independent sequence of execution, but threads of the main process run in the same memory space, managed independently by a scheduler.

- Every thread that is created in a program is given its own call stack, where it stores local variables references.
- However, all threads share the same heap, where the objects live in memory.

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

###### 1. Creating a class that extends `Thread class`

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

###### 2. Using Runnable Interface

Pass a lambda expression as the Runnable type required in the Thread constructor

```java
public class ThreadLambda {
  public static main(String[] args) {
    // passing lambda expression to Thread constructor
    Thread willRun = new Thread(() -> {
	  System.out.println("Running!");
	});
	willRun.start();
  }
}
```

> How can we implement multithreading in Java?

#### Example

`Employee.java`

```java
public class Employee extends Thread {

	@Override
	public void run() {

		for(int i = 0; i < 10; i++) {
			System.out.println(Thread.currentThread().getName() + " is working...");

			try {
				Thread.sleep(2000);
			} catch (InterruptedException e) {

				/*
				 * InterruptedException is thrown when the Employee's interrupt()
				 * method is called. We will break out if this occurs.
				 */
				e.printStackTrace();
				break;
			}
		}
	}
}
```

`ThreadDriver.java`

```java

public class ThreadDriver {

	public static void main(String[] args) {

		Employee emp1 = new Employee(); // Thread state: NEW
		emp1.setPriority(1);
//		emp1.run();	// does not actually create a new thread
		emp1.start(); // Thread state: RUNNING

		Employee emp2 = new Employee();
		emp2.setPriority(2);
		emp2.start();

		/*
		 * join() method
		 *
		 * Using join(), we tell our thread to wait until the specified thread completes
		 * its execution. There are overloaded versions of the join() method, which allows
		 * us to specify the time for which you want to wait for the specified thread to
		 * terminate.
		 */
		try {
			emp1.join(); // Waiting for emp1 to finish its execution
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		// Display the priority of threads. The default priority is 5.
		System.out.println(emp1.getPriority());
		System.out.println(emp2.getPriority());

		// Check to see if a given thread is alive or dead
		System.out.println(emp1.isAlive());
		System.out.println(emp2.isAlive());


	}
}
```

### Runnable interface

`java.lang.Runnable` is an interface that is to be implemented by a class whose instances are intended to be executed by a thread.

To create a class that implements the Runnable functional interface

- create a class the implements the `Runnable interface`
- implement the `run()` method
- pass an instance of your class to a `Thread constructor`
- call the `start()` method on the thread

```java
// create a class the implements the `Runnable interface`
public class MyRunnable implements Runnable {
  // implement the `run()` method
  @Override
  public void run() {
    System.out.println("Inside the MyRunnable class");
  }
}
```

Because Runnable is a functional interface, we can use a lambda expression to define thread behavior inline instead of implementing the interface in a separate class.

We pass a lambda expression as the Runnable type required in the Thread constructor.

```java
public class ThreadLambda {
  public static main(String[] args) {
    Thread willRun = new Thread(() -> {
	  System.out.println("Running!");
	});
	willRun.start();
  }
}
```

### important class members

### Thread states

> What are some states a thread can be in?

At any given time, a thread can be in one of these states:

- `New`: newly created thread that has not started executing
- `Runnable`: either running or ready for execution but waiting for its resource allocation
- `Blocked`: waiting to acquire a monitor lock to enter or re-enter a synchronized block/method
- `Waiting`: waiting for some other thread to perform an action without any time limit
- `Timed_Waiting`: waiting for some other thread to perform a specific action for a specified time period
- `Terminated`: has completed its execution

#### Runable State

- a thread might actually be running
- or it might be ready to run at any instant of time
- it is the responsibility of the thread scheduler to give the thread, time to run

A multi-threaded program allocates a fixed amount of time to each individual thread.

- each and every thread runs for a short while and then pauses
- and relinquishes the CPU to another thread so that other threads can get a chance to run.
- When this happens, all such threads that are ready to run, waiting for the CPU and the currently running thread lie in a runnable state.

#### Timed Waiting State

A thread lies in a timed waiting state when it calls a method with a time-out parameter. A thread lies in this state until the timeout is completed or until a notification is received. For example, when a thread calls sleep or a conditional wait, it is moved to a timed waiting state.

### Thread Class vs Runnable Interface

- If we extend the Thread class, our class cannot extend any other class because Java doesn’t support multiple inheritance. But, if we implement the Runnable interface, our class can still extend other base classes.
- We can achieve basic functionality of a thread by extending Thread class because it provides some inbuilt methods like `yield()`, `interrupt()` etc. that are not available in Runnable interface.
- Using runnable will give you an object that can be shared amongst multiple threads.

## Synchronization

_Know the following concepts at a high level:_

- Deadlock
- Livelock
- Producer-Consumer Problem

> What is synchronization?

Synchronization is the capability to control the access of multiple threads to any shared resource.

- In a multithreaded environment, a race condition occurs when 2 or more threads attempt to access the same resource.
- Using the `synchronized` keyword on a piece of logic enforces that only one thread can access the resource at any given time.
- synchronized blocks or methods can be created using the keyword.
- Also, one way a class can be "`thread-safe`" is if all of its methods are synchronized.

### Synchronized block

- Multi-threaded programs may often come to a situation where multiple threads try to access the same resources and finally produce erroneous and unforeseen results.

- So it needs to be made sure by some synchronization method that only one thread can access the resource at a given point in time. - - - Java provides a way of creating threads and synchronizing their tasks using synchronized blocks.
- Synchronized blocks in Java are marked with the synchronized keyword.
- A synchronized block in Java is synchronized on some object.

```java
// Only one thread can execute at a time.
// sync_object is a reference to an object
// whose lock associates with the monitor.
// The code is said to be synchronized on
// the monitor object
synchronized(sync_object)
{
   // Access shared variables and other
   // shared resources
}
```

- All synchronized blocks synchronize on the same object can only have one thread executing inside them at a time.
- All other threads attempting to enter the synchronized block are blocked until the thread inside the synchronized block exits the block.

#### monitors

This synchronization is implemented in Java with a concept called monitors.

- Only one thread can own a monitor at a given time.
- When a thread acquires a `lock`, it is said to have entered the monitor.
- All other threads attempting to enter the locked monitor will be suspended until the first thread exits the monitor.

### Deadlock

Deadlock occurs when one thread is waiting on a resource held by another thread, which is waiting on a resource the first has.

In this scenario, execution of both threads is blocked and the program is stuck indefinitely.

Though it is not possible to completely get rid of the deadlock problem, we can take precautions to avoid such deadlock conditions:

- By avoiding Nested Locks
- By avoiding unnecessary locks

#### Nested Locks

Nested locks mean we try to provide access to resources to multiple threads.

If we have already assigned one lock to a thread then we should avoid giving it to the another thread

#### Avoiding Unecessary Locks

We should also avoid giving locks to members or threads which do not need it. We should only provide the lock to the important threads and avoid using unnecessary locks.

If we provide an unnecessary lock to a thread that does not really need it, then it may cause a condition of deadlock.

#### Deadlock Example

There are two threads t1 and t2. Both threads are running concurrently (simultaneously). During execution, thread t1 is waiting for data that is locked by thread t2 and t2 is waiting for data that is locked by thread t1.

In this case, none of the threads will unlock the lock because of not completing their execution process. This situation is called deadlock.

When thread deadlock occurs in a program, the further execution of program will stop. Therefore, thread deadlock is a drawback in a program. We should take care to avoid deadlock while coding.

#### Solve Current Deadlock

- to get the PID of the process, we type `jps` command and then we get the PID of the running process.
- to get the thread dump we will write the `jcmd PID Thread.dump` command to detect the deadlock. We can also get this dump file in a text file.

### Livelock

> What is the difference between deadlock and livelock?

Livelock is concurrency problem and is similar to deadlock.

- In livelock, two or more threads keep on transferring states between one another instead of waiting infinitely as we saw in the deadlock example.
- Consequently, the threads are not able to perform their respective tasks.
- In a livelock condition thread are NOT blocked.

#### Livelock Example

A simple example of livelock would be two people who meet face-to-face in a corridor, and both of them move aside to let the other pass. They end up moving from side to side without making any progress as they move the same way at the time. Here, they never cross each other.

### Producer-Consumer Problem

> Producer-Consumer Problem

The Producer-Consumer problem is a classic example of a multi-process synchronization problem.

- Here, we have a fixed-size buffer and two classes of threads - producers and consumers.
  - Producers produces the data to the queue
  - Consumers consume the data from the queue.
  - Both producer and consumer shares the same fixed-size buffer as a queue.
- The producer should produce data only when the queue is not full.
  - If the queue is full, then the producer shouldn't be allowed to put any data into the queue.
- The consumer should consume data only when the queue is not empty.
  - If the queue is empty, then the consumer shouldn't be allowed to take any data from the queue.

We can solve the Producer-Consumer problem by using wait() & notify()methods to communicate between producer and consumer threads

- The `wait()` method to pause the producer or consumer thread depending on the queue size.
- The `notify()` method sends a notification to the waiting thread.

Producer thread will keep on producing data for Consumer to consume.

- It will use wait() method when Queue is full and use notify() method to send notification to Consumer thread once data is added to the queue.

```java
public synchronized void produce() {
	while (queue.size() == MAX_SIZE) {
		//Queue is full, Producer thread waiting for consumer to take data from the queue
		wait();
	}
	/* When queue has space, Producer produces the data and adds them into the queue.
	*  After that, Producer sends the notification to the Consumer.
	*/
	//producing data
	queue.add(data);
	notify();
}
```

Consumer thread will consume the data form the queue. It will also use wait() method to wait if queue is empty. It will also use notify() method to send notification to producer thread after consuming data from the queue.

```java
public synchronized String consume() {
	while (messages.isEmpty()) {
		//Queue is empty, Consumer thread waiting for producer to put data to the queue
		wait();
	}
		/* When queue has data, Consumer consumes the data and removes it from the queue.
		*  After that, Consumer sends the notification to the Producer.
		*/
		//consuming data
		queue.remove(data);
		notify()
}
```
