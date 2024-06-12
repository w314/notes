java, variable, casting, operators

# Java Variables
>A `variable` is a container for storing data.

## Variable Types

- `primitive data type` 
- `reference data type` - data types defined in the Java API or by a programmer
  - stores the reference to an object in memory
  - the type of a reference variable determines what types of objects a reference variable can store a reference to


### Primitive Data Types
> What is a primitive data type? Please list a few and explain them
- data types defined by the language
- stores the value of the data
- type defines the size, that defines the range of values the variable can store
- stored in the stack

Primitive Types in Java:

  - boolean
    - 1 bit
    - `true` or `false`
  - char
    - uses `''`
    - 2 bytes
  - numerical types (integers):
    - `byte`
      - 8-bit signed
      - range: -128 to 127
    - `short` 
      - 16-bit signed integer
      - range: -32,768 to 32,767
    - `int` 
      - 32-bit signed integer
      - range: -2to31 to 2to31
    - `long`
      - 64-bit signed integer
      - range -2to63 to 2to63
  - floating points
    - `float` 
      - 32-bit IEEE 754 floating point
    - `double` 
      - 64-bit IEEE 754 floating point

#### Using variables

```java
dataType variableName = value;
```

> What is the difference between assigning and declaring a variable?

- `Declaring` creates a place in memory to store information of that datatype.

- `Assigning` stores a value in the created memory place.

##### Variable Declaration

```java
datatype variableName;
```

- The `variable name` is the unique identifier used to reference that variable again
- Java is a strongly-typed language which means that all variables in Java must define what type of data we can store into that variable.
- This statement creates a place in memory for Java to store information of that specific datatype.
- camelCase naming convention

##### Assigning value to a variable

If we want to store a value in the variable:

```java
variableName = value;
```

- stores a value in the variable
- only work as long as the new variable is of the same datatype

## Opearators

- special symbols that perform a task
- use one or more operands, or values
- have precedence, just like math

### Operator Categories

- arithmetic
- assignment
- comparison
- logical

> What is the modulo operator? How is it useful?

### Assignment Operators

> What are shorthand assignment operators?

Assignment operators assign value to a variable.

= += -= \*= /= %= &= ^=

> How do you use increment and decrement operators?

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

## Casting

`Casting` is the process of converting a data type to another data type.
> What is explicit and implicit casting?


`implicit casting`

- AKA widening or upcasting
- automatically done by Java
- does it with primitive data types
- where there is no loss of data

  - If one of the values is a double, the other value is converted to a double
  - If neither is a double but one is a float, the other is converted to a float.
  - If neither is a double nor a float but one is a long, the other is converted to a long.
  - If all else fails, both values are converted to int.

`explicit casting`

- AKA narrowing or downcasting
- done by programmer
- uses `()`:

```java
int i = 200;
short s = (short)i;
```

- In some cases you will have to use the data type's own methods to convert. Some of these methods are listed in the table below.
  - `String` to `int` with `Integer.parseInt(String)`
  - `int` to `String` with `String.valueOf(int)`


## Questions
-  What is a variable?