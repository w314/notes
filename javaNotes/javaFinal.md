java, final


# `final` keyword
> Used to define an entity that cannot be changed.

- final variable
  - cannot be reassigned
  - but values in an array can still be changed
- final method
  - method cannot be overriden by a subclass
- final class
  - cannot be extended

Is this valid java?
```java
final int test;
test = 20;
```
YES, the variable test was not assigned a value when declared, so it can be assigned one later. (once)