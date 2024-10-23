java, interface, functional-interface

# Java Interface
> Interfaces in java are used to specify a set of methods that a class must implement.

- provides a way to achieve abstraction
- povides a way for multiple inheritance

## Key Features

- `abstract methods`
  - methods without body
  - `abstract` keyword is not needed
  - must be implemented by classes that implement the interface
- `default methods`
  - methods with default implementation
  - can be overriden
- `static methods`
  - include method body
  - are NOT inherited by implementing classes
  - has to called on the interface itself
- `private methods`
- `constants`
  - they are implicitely
    - public
    - static
    - final
- multiple inheritance
  - classes can implement multiple interfaces

## Inheritance

- an interface can `extend` more than one interface
- a class can `extend` a class AND `implement` more then one interface

### `sealed` interface

Addresses concerns related to unrestricted inheritance

The `sealed` modifier in the interface declaration restricts which classes can implement the interface. 

The `permits` clause specifies these classes.

```java
sealed interface Pet permits Dog, Cat {}
```

## Interface Methods
All interface methods are implicitely `public`  

### Default Methods

- Make it possible to add additional methods in the interface without disturbing the classes which have already implemented the interface.
- provides backwards compatibility
- if a class inherits from multiple interfaces that have the same default methods (same method signature)
  - code won't compile
  - class must provide implementation for those methods

```java
public interface Alarm {
  default String turnAlarmOn() {
    return "Turning alarm on";
  }
}

public interface Vehicle {
  default String turnAlarmOn() {
    return "Alarm is turned on";
  }
}

// class inherits both interface
public class Car implements Vehicle, Alarm {

  // must override default method
  // found in both interface
  @Override
  public String turnAlarmOn() {
    // using default from Vehicle class
    // could also call both class
    // or choose any other implementation
    return Vehicle.super.turnAlarmOn();
  }
}
```

## Marker or tagged interface

An interface which has no member is known as a marker or tagged interface, for example, Serializable, Cloneable, Remote, etc. They are used to provide some essential information to the JVM so that JVM may perform some useful operation.

## Questions
> Why would you use an interface over an abstract class?

Interfaces advantages over class:
  - Implementation details do not need to be provided in the interface.
  - A class can only extend one other class, but it can implement as many interfaces as needed.

