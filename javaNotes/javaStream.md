# Stream

The Arrays.stream() method in Java does not support char[] because there is no CharStream in Java's Stream API. The Stream API provides specialized streams for int[], long[], and double[] (IntStream, LongStream, and DoubleStream, respectively), but not for char[].




The Stream API is a functional-style way of defining operations on a stream of elements.

- the Stream API allows you to create pipelines, or sequences of aggregate operations, on streams of data.
- `Stream` : sequence of data
- Streams do not STORE the data (like collections), they move the elements through the pipeline
- Streams do not manipulate the original source of data
- functional programming - useful for completing a series complex tasks on the data to get a result

- Streams are an abstraction which allow defining operations which do not modify the source data and are lazily executed.
- Some built-in Streams are located in the java.util.stream package.
- Streams are divided into intermediate and terminal operations.
  - `Intermediate Operations` return a new stream and are always lazy - they don't actually execute until a terminal operation is called.
  - `Terminal Operations` trigger the execution of the stream pipeline, which allows efficiency by perfoming all operations in a single pass over the data.
- `Reduction Operations` are terminal operations that take a sequence of elements and combine them into a single result.
  - Stream classes have the `.reduce()` and `.collect()` methods for this purpose, with many built-in operations defined in the `Collectors` class.

### Pipelines

- require a source of data, like a collection
- can contain zero or more intermediate operations

### terminal vs intermediate operations

In the Java Stream API, intermediate operations are operations which are lazily executed and return another Stream and terminal operations are operations which initiate the execution when invoked .

> What are intermediate stream operations?

> What are terminal stream operations?

### common intermediate operations

- produce a new stream
- filter()
- map()
- sorted()

### common terminal operations

Produces a non-stream value OR no value at all

- forEach()
- reduction operations

#### reduction operations

A type of `terminal operation` that produce a single result.

- reduce()
- max()
- min()
- average()
- collect() uses the help of the Collectors class for a more specific return value

### Example

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