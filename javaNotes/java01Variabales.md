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

## Opearators

- special symbols that perform a task
- use one or more operands, or values
- have precedence, just like math

### Operator Categories

- unary (`++`, `--`, `~`, `!`)
- arithmetic
- relational
- logical (`&&`, `||`, `!`)
- ternary
- assignment
- bitwise


### Operator Precedence
- paraenthesesis (`()`)
- postfix `++`, `--`
- unary, prefix `++`, `--`, `+`, `-`, `~`, `!`
- mulitplicative `*`, `/`, `%`
- additive `+`, `-`
- shift `<<`, `>>`, `>>>`
- relational `<`, `>`, `<=`, `>=`
- equality `==` `!=`
- logical AND `&&`
- logical OR `||`
- ternary `?:`
- assigment `=`, `+=`, `<<=`, ...


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

### Logical Operators
- there is no unsigned left shift opearator `<<<` in Java


### bitwise operators

#### `~`

```java
int num = 5; // Binary representation of 5: 0000 0101
int result = ~num; // This inverts each bit: 1111 1010
System.out.println(result); // This will print the decimal equivalent of the inverted binary
```
- given that int is a 32-bit type in Java, the actual binary representation of 5 is `0000 0000 0000 0000 0000 0000 0000 0101`
- `~num` would be `1111 1111 1111 1111 1111 1111 1111 1010`
-  when converted to decimal, this represents `-6` because Java uses `two's complement notation` for negative numbers.

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


## Questions
-  What is a variable?