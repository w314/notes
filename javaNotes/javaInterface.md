java, interface, functional-interface

# Interfaces
An interface is used to define a generic template that can be implemented by various classes. 
- used to simulate multiple inheritance
- an interface can `extend` more than one interface
- a class can `extend` a class AND `implement` more then one interface


> Why would you use an interface over an abstract class?

- A class implements an interface using the `implements` keyword in the class definition and by providing implementations for any abstract methods defined by the interface.

Interfaces advantages over class:
  - Implementation details do not need to be provided in the interface.
  - A class can only extend one other class, but it can implement as many interfaces as needed.

## Interface contains
1. methods signatures
    - by default interface methods are implicitly
      - `public`
      - `abstract` (no need to declare them `abstract`)
    - since Java 9 can also have
        - `private` methods
        - `default` methods
        - `static` methods
2. constant declarations
    - all interface variables are implictly `public`, `static` & `final`
    - i.e. constants

### `default` implementation methods
- using the `default` keyword allows us to provide an implementation for that method
- With this, we can add additional methods in any interface without disturbing the classes which have already implemented the interface
- implementing classes CAN override the method

### `static` implementation methods

- using `static` also allows us to provide implementation
- implementing classes CANNOT override `static` methods


## `sealed` interface
- introduces in Java 15
- addresses concerns related to unrestricted inheritance

The `sealed` modifier in the interface declaration restricts which classes can implement the interface. 

The `permits` clause specifies these classes.

```java
sealed interface Pet permits Dog, Cat {}
```

