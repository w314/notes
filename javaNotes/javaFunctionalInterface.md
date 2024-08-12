java, functional-interface, 

# Functional Interface
> Any interface that has only one abstract method.

- special case of regular interface
- has only one abstract method
- there are many built-in functional interfaces in `java.util.function`

### `@FunctionalInterface`
- no need to include the annotation 
- if included the compiler checks that there is only one abstract method

```java
@FunctionalInterface
interface Calculator {
    int do(int x int y);

    default boolean isPositive(int x) {
        return x > 0;
    }
}
```

## User Defined Functional Interface

## Built In Funcional Interface
Java provides a series of inbuilt functional interfaces.

### Function
> Represents a function that takes a single input parameter and returns a single value/object.

```java
Function<Long, Long> addNum = (value) -> value + 10;
```

### Predicate
>It represents a function that takes a single value/object as a parameter, and returns true or false.
```java
Predicate<Integer> checkAge = (age) -> age > 18;
```

- functional interface,  part of the `java.util.function`
- has a single argument function
- returns a boolean value
- are often used for filtering o  List<Integer> list10 = new ArrayList<>(Arrays.asList(2, 3, 6));
r matching objects based on certain criteria

Key Characteristics:
- **Functional Interface**: It has a single abstract method, `test(T t)`, which evaluates the predicate on the given argument of type T and returns a boolean value.
- **Generic**: It is a generic interface, meaning it can be used with any type of object.

Method Signature:
```java
boolean test(T t)
```

Common Uses:
- **Filtering Collections**: Used with Stream API for filtering collections based on a condition.
- **Conditional Checks**: Simplifies conditional logic by encapsulating conditions into reusable predicates.
- **Combining Predicates**: Predicates can be combined using logical operations like and, or, and negate to create complex conditions.

Example Usage:
```java
import java.util.function.Predicate;
import java.util.stream.Collectors;
import java.util.List;
import java.util.Arrays;

public class PredicateExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "Diana");

        // Predicate to check if a name starts with 'A'
        Predicate<String> startsWithA = name -> name.startsWith("A");

        // Using the predicate to filter names
        List<String> namesStartingWithA = names.stream()
                                               .filter(startsWithA)
                                               .collect(Collectors.toList());

        System.out.println(namesStartingWithA); // Output: [Alice]
    }
}
```
In this example, a Predicate<String> is defined to test whether strings start with the letter "A". This predicate is then used to filter a list of names using the Stream API, collecting and printing names that satisfy the predicate.

### Supplier
>It represents a function that produces a value/an object without taking any input parameter.

```java
Supplier<Integer> generateRandom = ()-> new Integer((int) (Math.random() * 100));
```

### Consumer
>It represents a function that consumes or processes a value/an object without returning anything. 

```java
Consumer<String> printValue = (name)-> System.out.println(name);
```

