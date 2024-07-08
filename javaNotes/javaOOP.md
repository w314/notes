java, oop

- whenever a new object is created with teh `new` keyword all its instance variables are initialized to the default value of their types

What is the output of this code:
```java
class Trainee {
    int id;
}

public class Main {
    public static void main(String[] args) {
        Trainee trainee = null;
        System.out.println(trainee.id);
    }
}
```
It is a `runtime error`, it is not checked at compilation time.


## Relationships between classes

- Aggregation - has a
- Association - uses a  
- Inheritance -


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