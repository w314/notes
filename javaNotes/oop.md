## Classes and Objects

### Class

> What are classes used for?

A class is a template used to instantiate objects.

A class used as the `type` for a `reference variable` determines what behaviors of an object can be invoked, and how any variables get initialized.

We use classes to create a blueprint for objects.

### Object

> Describe what an object is.

An object is an instance of a class in memory.

- In Java, you never interact with objects directly. Instead, you interact with them through their reference, which is the memory address used by the JVM to find a particular object.

- constructor declares how an object is to be instantiated and initialized from the class "blueprint".

### Constructur

> What is a constructor and how is it different from a method?

A `constructor` is a special method that declares how an object is to be instantiated and initialized from the class "blueprint".

- A constructor is declared like a method, except its method signature does not contain a return type, and a constructor always has the same name as the class.

- The new object created by the constructor is always of the class in which the constructor is declared.
  this refers to the object which is being instantiated - it is used to initialize instance variables, or - to call other constructors (this is called constructor chaining)
  There is another keyword important for constructors - the super keyword, which references the "super", or parent, class.
  When invoked as a method (super()), the parent class constructor will be called.
  A super() call (or a this() call) must be the first line of any constructor.
- If not explicitly provided, the compiler will inject super() it on the first line implicitly.
  The "default" constructor takes no arguments and simply calls super() (see above) - sometimes it is referred to as the "default, no-args" constructor.
- However if we define our own constructor(s) in the class, we will not receive a default constructor from the compiler.

#### Constructors vs. Methods

- have no return types
- have same name as class
- provide no functionality to object
- automatically called at object creation when a class is instanceated

## OOP Principles

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

> Describe abstraction and how would you use it in a project?

`Abstraction` is an OOP programming principle.

Through abstraction we hide underlying complexity through a simplified interface.

example: Shape class, getArea() method

### Polymorphism

> Describe polymorphism and how would you use it in a project?

`polymorphism` means "taking on many forms". In OOP polymorphism provides the means to perform a single action in multiple different ways

The most common examples of polymorphism:

- method overloading
- method overriding
- upcasting
- downcasting

#### `method overloading`

Within a class when there are two or more methods in a class with the same method name, but different method signatures by changing the parameter list.

- change in number of parameters
- change in types of parameters
- compile time / static polymorphism

#### `method overriding`

when a method in a child class has the same method signature as a method in the parent class, but with a different implementation

- make class hierarchies more flexible and dynamic
- runtime / dynamic polymorphism
- `static methods` cannot be overriden
- return type can only be changed if it is a subtype of the original type (`covariant return types`)
- access modifier can be changed but must provide more _not less_ access

`virtual method invocation` when variable is declared as type Animal but refers to a Dog object, calling the method spead will use Dog's implementation of the method

#### `upcasting`

is the process of casting an object of a subclass to an object of its superclass

- done automatically by the Java compiler
- safe operation does not involve loss of data
- you can access only the members of the superclass, but don not lose any members of the subclass

#### `downcasting`

The process of casting an object of a superclass to an object of its subclass

- risky, may result in `ClassCastException` if the object being cast is not actually an instance of the subclass
- use `instanceof` operater to check before downcasting

EXAMPLE
method overloading - temperature converter working with both integers, doubles or string

method overriding - speak method implemented differently in Animal subspecies

### Encapsulation

> Describe encapsulation and how would you use it in a project?

- `encapsulation` is a process of wrapping data and methods in a single unit.
- it is an OOP principle
- in OOP data and methods operating on that data are combined together to form a single unit, which is referred to as a Class
- `encapsulation` is as a protective wrapper that prevents the code and data from being arbitrarily accessed by other code defined outside the wrapper.

> `encapsulation` means **restricting access to data members** by using access modifiers and getter/setter methods

When encapsulating your code, certain conventions should be followed:

- All instancce fields for a class should be private
- Each field should have getters and setters as needed (typically these are public, but other access modifiers can be used as needed).
- Getter and Setter Methods (a.k.a. 'accessor' and 'mutator' methods) should use the following name convention:
  - getVariableName
  - setVariableName

EXAMPLE
employee object, make slary private, setSalary checks valid salary number, getSalary check is user has access rights

### 56 How is method overriding different from method overloading?

### 58 What is the purpose of using getter and setter methods?

### 59 Why would you use an interface over an abstract class?

Interfaces have these advantages over class:

- Implementation details do not need to be provided in the interface.
- A class can only extend one other class, but it can implement as many interfaces as needed.
