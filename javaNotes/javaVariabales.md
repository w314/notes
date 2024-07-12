java, variable, casting, operators

## Java Variables
>A `variable` is a container for storing data.

>`Identifier` is a name given to a variable, method or class to identify it.

Identifier name NOs: 
- cannot start with a digit
- should have no spaces
- should not be a Java keyword

Identifier name YES-s 
- can contain:
  - `a-z`, `A-Z`, `0-9`, `$`,`_`
- must begin with
  - `a-z` or `A-Z`
  - underscore `_`
  - dollar sign `$`
- case sensitive
- no length restriction


Types:
  - `primitive data type` 
  - `reference data type` - data types defined in the Java API or by a programmer
    - stores the reference to an object in memory
    - the type of a reference variable determines what types of objects a reference variable can store a reference to
    - default value of an object reference is `null`



## Primitive Data Types
> What is a primitive data type? Please list a few and explain them
- data types defined by the language
- stores the value of the data
- type defines the size, that defines the range of values the variable can store
- stored in the stack

Primitive Types in Java:

### `boolean`
  - 1 bit
  - `true` or `false`
  - default value: `false`

### `char`
  - uses `''`
  - 2 bytes
  - default value: 0

### numerical types
- for integers
- default value: 0
- types:
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

`Two's complement notation`:
- most common way to encode negative numbers in binary number systems
- `**positive numbers**: represented as usual binary
- **negativ numbers**: represented by inverting all the bits of it's positiv conunterpart and than adding one to the reult (except the lowest negative number that directly represents itself, as it's positive counterpart would be out of range)
- **zero**: 0000...000, and its negative is itself
- **Range** an `n` bit number can represent values from `-2^(n-1)` to `2^(n-1) - 1` (an 8 bit number can represent values from -128-127)

```java
// decimal 5 in an 8-bit system
0000 0101

// calculate -5
// first invert the bits of positive 5
1111 1010
// add 1, the result represents -5
1111 1011
```

### floating points
- default value: 0.0
- types:
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

## Casting

`Casting` is the process of converting a data type to another data type.
> What is explicit and implicit casting?


### `implicit casting`

- AKA widening or upcasting
- automatically done by Java
- does it with primitive data types
- where there is no loss of data


- `char` -> `int`


### `explicit casting`

- AKA narrowing or downcasting
- done by programmer
- uses `()`:

```java
int i = 200;
short s = (short)i;
```
examples
```java
float floatVar = 12.7f;
int intVar = floatVar; 
// would give incompatible type error
int intVar1 = (int) floatVar;
System.out.println(intVar1) // 12
// decimal part gets cut
// if float holds value larger than fits into int
// the result will be the max value int can hold 



```

- In some cases you will have to use the data type's own methods to convert. Some of these methods are listed in the table below.
  - `String` to `int` with `Integer.parseInt(String)`
  - `int` to `String` with `String.valueOf(int)`




## Wrapper Classes

- every primitive has a corresponding object type
- mainly useful when working with Collections

#### Autoboxing

> What is autoboxing and unboxing?

- `Boxing` - the process of converting a primitive to its wrapper clas
- `Unboxing` is the reverse - converting a wrapper class to its primitive.
- `autoboxing` - a feature in which both boxing and unboxing done implicitly by Java. Example: when passing an `int` variable as parameter to a function requesting an `Integer`
- Wrapper classes have static helper methods like .parseX() and .valueOf() for explicit primitive conversion.


Values of which of the following types can be passed to the method below?
- String
- int
- boolean
```java
public static void show(Object obj) {
  System.out.println(obj);
}
```
All, int, boolean will be autoboxed.

## Questions
-  What is a variable?