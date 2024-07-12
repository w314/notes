
java, operators

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
