## Object Oriented Programming

- approach to solving programming problems by creating entities that model real-world objects
- these entities, called objects, can interact with one another

## Classes and Objects

### Class

A class is a template used to instantiate objects.

#### Class members:

- variables
- methods
- constructors

##### static vs. instance members

- Variables and methods that are NOT static are instance members.
- instance members are copied by objects and can only be interacted with using an object of the class
- instance variables are known as "state" that objects can have
- instance methods are known as "behavior" that objects can have

> What are classes used for?

A class used as the `type` for a `reference variable` determines what state and behavior an object will possess.

We use classes to create a blueprint for objects.

### Object

> Describe what an object is.

An object is an instance of a class in memory.

- It has `state`(instance variables) and `behavior` (instance methods).

- In Java, you never interact with objects directly. Instead, you interact with them through their reference, which is the memory address used by the JVM to find a particular object.

- the `constructor` declares how an object is to be instantiated and initialized from the class "blueprint".

### Constructur

> What is a constructor and how is it different from a method?

A `constructor` is a special method that declares how an object is to be instantiated and initialized from the class "blueprint".

- special method defined in a class
- initializes the state of a newly created object
- has no return type
- name is the same of the class
- the new object created by the constructor is always of the class in which the constructor is declared
- you can have more than one constructor IF they have different parameter lists

#### `this`Keyword

The `this` keyword refers to the object which is being instantiated - it is used to initialize instance variables, or - to call other constructors (this is called constructor chaining)

#### `super` Keyword

- the `super` keyword references the "super", or parent class.

  - When invoked as a method (super()), the parent class constructor will be called.
  - A super() call (or a this() call) must be the first line of any constructor.

- If not explicitly provided, the compiler will inject super() it on the first line implicitly.

#### Default Constructor

- if you do not add a constructor to your class a `no-args` constructor is created for you behind the scenes
- this `default constructor` takes no arguments and simply calls super()
- however if we define our own constructor(s) in the class, we will not receive a default constructor from the compiler.

#### Constructors vs. Methods

- have no return types
- have same name as class
- provide no functionality to object
- automatically called at object creation when a class is instanceated

## OOP Features

- Inheritance
- Abstraction
- Encapsulation
- Polymorphism

### Inheritance

> Describe inheritance and how would you use it in a project?

`Inheritance` is inheriting the common state and behavior of parent class (super class) by its derived class (sub class or child class).
A sub class can inherit all non-private members from super class, by default.

Types:

- `single`
- `multi-level`
- `hierarchical`: one super class with more than one subclasses
- `multiple`: inherit from more than one parent (NOT POSSIBLE IN JAVA)

Example:
Animal -> Cat, Dog

```java
class Animal {
  ...
}

class Dog extends Animal {
  ...
}
```

> What state and behavior would you define in a parent class but not a subclass?

Example:
Animal:
age, name, abstract makeNoise, sleep

> What state and behavior would you define in a subclass but not in the parent class?

Example
Animal:
age, name, abstract makeNose, sleep
Dog: growl

### Abstraction

`Abstraction` means hiding implementation details through a higher-level construct, like abstract classes and interfaces, thereby decreasing coupling and increasing cohesion.

> Describe abstraction and how would you use it in a project?

`Abstraction` is an OOP programming principle.

Through abstraction we hide underlying complexity through a simplified interface.

example: Shape class, getArea() method

### Polymorphism

`Polymorphism` mean allowing the implementation of a given behavior to vary, whether between subclasses or within the same class.

> Describe polymorphism and how would you use it in a project?

`Polymorphism` means "taking on many forms". In OOP polymorphism provides the means to perform a single action in multiple different ways.

The most common examples of polymorphism:

- method overloading
- method overriding
- upcasting
- downcasting

> How is method overriding different from method overloading?

#### `method overloading`

Within a class when there are two or more methods in a class with the same method name, but different method signatures by changing the parameter list.

- change in number of parameters
- change in types of parameters
- compile time / static polymorphism

EXAMPLE
method overloading - temperature converter working with both integers, doubles or string

#### `method overriding`

when a method in a child class has the same method signature as a method in the parent class, but with a different implementation

- make class hierarchies more flexible and dynamic
- runtime / dynamic polymorphism
- `static methods` cannot be overriden
- return type can only be changed if it is a subtype of the original type (`covariant return types`)
- access modifier can be changed but must provide more _not less_ access

`virtual method invocation` when variable is declared as type Animal but refers to a Dog object, calling a method will use Dog's implementation of the method

EXAMPLE of method overriding - speak method implemented differently in Animal subspecies

#### `upcasting`

is the process of casting an object of a subclass to an object of its superclass

- done automatically by the Java compiler
- safe operation does not involve loss of data
- you can access only the members of the superclass, but don not lose any members of the subclass

#### `downcasting`

The process of casting an object of a superclass to an object of its subclass

- risky, may result in `ClassCastException` if the object being cast is not actually an instance of the subclass
- use `instanceof` operater to check before downcasting

### Encapsulation

`Encapsulation` means **restricting access to data members** by using:

- access modifiers
- getter/setter methods

> Describe encapsulation and how would you use it in a project?

> What is the purpose of using getter and setter methods?

- `encapsulation` is a process of wrapping data and methods in a single unit.
- it is an OOP principle
- in OOP data and methods operating on that data are combined together to form a single unit, which is referred to as a Class
- `encapsulation` is as a protective wrapper that prevents the code and data from being arbitrarily accessed by other code defined outside the wrapper.

When encapsulating your code, certain conventions should be followed:

- All instancce fields for a class should be private
- Each field should have getters and setters as needed (typically these are public, but other access modifiers can be used as needed).
- Getter and Setter Methods (a.k.a. 'accessor' and 'mutator' methods) should use the following name convention:
  - getVariableName
  - setVariableName

EXAMPLE
employee object, make slary private, setSalary checks valid salary number, getSalary check is user has access rights

## SOLID Design Principles

Set of rules and best practices to follow in OOP class design.

> What are the SOLID design principles and why are they important?

- SRP - Single Responsibility Principle
- OCP - Open Closed Principle
- LSP - Liskov Substitution Principle
- ISP - Interface Segregation Principle
- DIP - Dependency Inversion Principle

### `Single Responsibility Principle (SRP)`

- A class should have only one purpose, focusing on a single responsibility or task.
- EXAMPLE: pulling data from a server, manipulating and storing it in a database is not single responsibility

### `Open-Closed Principle (OCP)`:

- Software entities should be open for extension but closed for modification
- you should be able to **add new functionality
  to a system without modifying its existing** code
- we use `abstract classes` and `interfaces` to achieve the `Open Close Principle`
- EXAMPLE: have an abstract area method in a shape class, that can be implemented differentle in triangles and squares, rather than if statements in shape class that have to be modified any time a new shape is introduced

### `Liskov Substitution Principle (LSP)`

- Objects of a superclass should be replaceable with objects of their subclasses
- any instance of a base class should be able to be replaced by an instance of a subclass without affecting the correctness of the program
- This means that, given that class B is a subclass of class A, we should be able to pass an object of class B to any method that expects an object of class A and the method should not give any weird output in that case.
- This is the expected behavior, because when we use inheritance we assume that the child class inherits everything that the superclass has. The child class extends the behavior but never narrows it down.
- EXAMPLE:

### `Interface Segregation Principle (ISP)`

- is about separating interfaces, many client-specific interfaces are better than one general-purpose interface
- Clients should not be forced to depend on interfaces they do not use
- EXAMPLE vehicle interface with opendoors() method and Bike class implementing vehicle interface and mock implement opendoors() method

### `Dependency Inversion Principle (DIP)`

- our classes should depend upon interfaces or abstract classes instead of concrete classes and functions
- if the `OCP (Open Closed Principle)` is the goal of `OO` architecture, `DIP (Dependency Inversion Principle)` is the primary mechanism to achive it
