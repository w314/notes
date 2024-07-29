java, polymorphism, method overloading, method overriding


## Polymorhism 

IMPORTANT EXAMPLE

```java
class Bike {
    int speedLimit = 90;

    public void ride() {
        System.out.println("Riding a bike");
    }
}

class Honda extends Bike{
    int speedLimit = 150;

    public void ride() {
        System.out.println("Riding a honda");
    }

}

class Main {
    public static void main(String[] args) {
        Bike bike = new Bike();
        Honda honda = new Honda();
        Bike hondaBike = new Honda();

        System.out.println("Bike's speed limit: " + bike.speedLimit);
        System.out.println("Honda's speed limit: " + honda.speedLimit);
        System.out.println("HondaBike's speed limit: " + hondaBike.speedLimit);

        bike.ride();
        honda.ride();
        hondaBike.ride();    }
}
```
Result:
Bike's speed limit: 90
Honda's speed limit: 150
HondaBike's speed limit: 90
Riding a bike
Riding a honda
Riding a honda

Reason:

Java accesses fields based on the reference type, while methods are invoked based on the actual object's type

- hondaBike is type Bike as it is declared `Bike hondaBike`
- it can reference an object of class `Bike` or any of its subclasses
- `new Honda()` creates a new instance of Honda (assigning the new Honda() object to a Bike reference is an example of polymorphism)
- at runtime Java runtime will use the actual objects (Honda) method if they were overwritten (polymorphism)
- field however are accessed based on the reference type, Java treats fields different than methods with respect to polymorphism


## Dynamic Binding
>Dynamic binding in Java is a mechanism by which a call to an overridden method is resolved at runtime, rather than compile-time. 
- This is a key aspect of polymorphism in object-oriented programming. 
- In Java, dynamic binding works with instance methods (not static methods or variables) 
- allows a program to use overridden methods of derived classes through references of parent class types.

In this example, even though the reference type is Animal, the sound method of Dog is called. 
- This is because the type of the actual object (Dog) determines which sound method to execute, demonstrating dynamic binding.
- HOWEVER there is no dynamic binding for instance variables and the parent class variables are used
```java
class Animal {
    int age = 2;
    void sound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    int age = 5;
    @Override
    void sound() {
        System.out.println("Dog barks");
    }
}

class Main {
    public static void main(String[] args) {
        Animal myAnimal = new Dog(); // Upcasting
        myAnimal.sound(); // Dynamic binding happens here
        // result: Dog barks
        System.out.println("My animal's age is: " + myAnimal.age); 
        // result: My animal's age is: 2
    }
}
```


## Examples

What is the output?
```java
class Parent {
    String str1 = "a";

    public Parent() {
        parentMethod();
    }

    void parentMethod() {
        System.out.println("Parent's parentMethod is called.");
        System.out.println(str1 + " ");
    }
}

class Child extends Parent {
    String str2 = "b";

    void parentMethod() {
        System.out.println("Child's parentMethod is called");
        System.out.println(str2 + " ");
    }
}


class Main {
    public static void main(String[] args) {
        Child child = new Child();
        child.parentMethod();
    }
}
```
Child's parentMethod is called
null 
Child's parentMethod is called
b 
- due to method overriding the parent constructor call the child's class method
- at this point the the child's class variables are not initialized yet
- after colling super constructor child class variables get initiated