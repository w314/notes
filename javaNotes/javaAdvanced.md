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

## Stream API

> What is the Stream API and what is it used for?

The Stream API is a functional-style way of defining operations on a stream of elements.

### terminal vs intermediate operations

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

## Threads

> What is a thread?

> How can we create a thread?

> How can we implement multithreading in Java?

### Thread class and Runnable interface

### important class members

### Thread states

> What are some states a thread can be in?

### concurrency

## Synchronization

_Know the following concepts at a high level:_

- Deadlock
- Livelock
- Producer-Consumer Problem

> What is synchronization?

> What is the difference between deadlock and livelock?

### Producer-Consumer Problem

> Producer-Consumer Problem
