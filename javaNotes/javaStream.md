# Stream API
> Way to deliver data. ( while Collections are a way to store data. )

`stream` : sequence of data

- a functional-style way of defining operations on a stream of elements
- do not manipulate the original source of data
- stream operations are lazily executed
- some built-in Streams are located in the java.util.stream package
- there is no CharStream in Java's Stream API (you CANNOT do `Arrays.stream()` on `char[]`)


### Stream Operations
Stream operatiosn are divided into intermediate and terminal operations.

#### `Intermediate Operations`
Return a new stream and are always lazy - they don't actually execute until a terminal operation is called.

- filter()
- map()
- sorted()

#### `Terminal Operations` 
- Trigger the execution of the stream pipeline, which allows efficiency by perfoming all operations in a single pass over the data.
- Produces a non-stream value OR no value at all

Common Terminal Operations:
- forEach()
- `Reduction Operations` 
  - take a sequence of elements and combine them into a single result
  - reduce()
  - max()
  - min()
  - average()
  - collect() uses the help of the Collectors class for a more specific return value

## Examples

```java
// get the names of all female employees
Employee.persons.stream()
.filter(Employee::isFemale)
.map(Employee::getName)
.forEach(System.out::println);

// get the names of all male employees who earn more than 5001.0
Employee.persons.stream()
.filter(Employee::isMale)
.filter(p -> p.getIncome() > 5001.0)
.map(Employee::getName)
.forEach(System.out::println);


double
```

Old examples:
```java
//Filter
public void streamFilter(List<Associate> associateList, String filter) {
  //Filter receives a Predicate<T> as parameter
  associateList
    .stream()
    .filter((Associate a) -> new StringBuilder(a.getFirstName()).indexOf(filter) != -1)
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

## Built-In Streams

Java provides several built-in stream types primarily in the `java.util.stream` package, designed to work with sequences of elements. These streams support a wide range of operations which can be pipelined to produce the desired result. The primary built-in streams in Java are:

1. **Stream<T>**: A stream of objects of type `T`. It's the most generic stream type, capable of holding any object types.

2. **IntStream**: A stream of primitive `int` values. This stream supports additional aggregate operations like `sum()`, `average()`, etc., specific to int values.

3. **LongStream**: Similar to IntStream, but for long values. It also supports operations like `sum()`, `average()`, and so on, tailored for long values.

4. **DoubleStream**: This stream is for `double` values and, like `IntStream` and `LongStream`, supports operations that are specific to `double` values, such as `sum()`, `average()`, etc.

These streams can be created in various ways, such as from collections, arrays, or specific methods like `range()`, `of()`, etc. They support operations that are classified as intermediate (operations that return a stream, such as `filter()`, `map()`) and terminal (operations that close the stream and produce a result, such as `collect()`, `forEach()`, `reduce()`).

Additionally, there's a special kind of stream known as `Stream.Builder<T>`, which is used to build streams by adding elements individually and then calling `build()` to create a `Stream<T>`.

## Questions

- What is a Stream in Java?
- What is the difference between a Stream and a Collection?
- What are intermediate and terminal operations in a Stream?
- What are some common intermediate operations in a Stream?
- What are some common terminal operations in a Stream?
- What is a reduction operation in a Stream?
- What are some common reduction operations in a Stream?
- What is the difference between intermediate and terminal operations in a Stream?
- What is the difference between a reduction operation and a terminal operation in a Stream
- What is the Stream API and what is it used for?