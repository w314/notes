java, interface

# Java Interface

An interface is similar to an abstract class, but there's a key difference: A class can only inherit one other class, but a class can implement as many interfaces as it needs.

A class `implements` an interface using the implements keyword in the class definition and by providing implementations for any abstract methods defined by the interface.

Interfaces have these advantages over inheritance:

- Implementation details do not need to be provided in the interface.
- A class can only extend one other class, but it can implement as many interfaces as needed.
  An interface acts as a contract for behaviors that a class can implement.

An interface acts as a contract for behaviors that a class can implement.

```java
public interface InterfaceA {
 public void methodName(); //You don't implement the method!
}
```

Interfaces have implicit modifiers on methods and variables.

- `Methods` are '`public`' and '`abstract`'
- `Variables` are '`public`', '`static`', and '`final`'

To inherit interfaces, a class MUST `implement` them and they are REQUIRED to implement all methods, unless the class is abstract.

## Interface inheritance

A class implements an interface, but one interface can extend another interface.

## Java 8

- we can have the method body in the interface. But we need to make it the default method
- we can have a static method in an interface

## Marker or tagged interface

An interface which has no member is known as a marker or tagged interface, for example, Serializable, Cloneable, Remote, etc. They are used to provide some essential information to the JVM so that JVM may perform some useful operation.
