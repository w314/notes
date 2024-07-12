java, enum

# Enum

> `Enum` is a data type which contains a fixed set of constant values.

- all enums implicitly the extend `java.lang.Enum` class
- enum fields are implicitely `static` and `final`
- they are instances of their enum type constructed when the enum type is referenced the first time
- enums are reference-types like classes and interfaces in Java, hence
    - can have constructors
    - can have methods
    - can have variables
- enum values can be used in `if` or `switch` statements

### `.values()`

- static method `values()` is automatically generated for each enum that returns an array of all the constant values defined inside them

### `.ordinal()`
- returns the ordinal of the enumeration constant
- it is its position in its enum declaration
- starting with 0

### Examples

```java
// NO = in declaration
public enum PizzaSize { SMALL, MEDIUM, LARGE };

// use enum type above
private PizzaSize size;

// using enum in if statement
if(this.size.equals(PizzaSize.MEDIUM)) {
    System.out.println("Size is medium");
}

// using enum is switch statement
PizzaSize size  = PizzaSize.MEDIUM
double discount = 0;

switch(size) {
    case SMALL:
        discount = 10;
        break;
    case MEDIUM:
        discount = 15;
        break;
}

// looping through enums
for(PizzaSize psize : PizzaSize.values()) {
    System.out.println(psize + " "  + psize.ordinal());
}

```

What should be added in the blank to get the output as "see"?
```java
class A {
    public enum show { see, saw }
}


class Main {
    public static void main(String[] args) {
        Test.show value = _________;
        System.out.println(value);
    }
}
```
`Test.show.see`

NOT new Test().show.see
