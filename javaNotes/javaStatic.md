java, static

# `static` Keyword

- static is a non-access modifier
- mainly used for memory management
- belongs to the class not to the class intances
    -  used to share the same variable or method of a given class.
    - a static memeber can be accessed before any objects of its class are created, and without reference to any object.

Static class members can be
- variables
- methods
- static blocks

> What is the difference between calling an instance method and a static method?


## Static Varibales
```java
// declare and intialize
private static float discount = 12.5f;

// initialize wiht static block
private static float tax;

static {
    tax = 8.5f;
}
```

- when a variable is declared static, then a single copy of the variable is created and it is shared among all objects at the class level


## Static Blocks
- used to initialize static variables when computation needed to intialize them
- gets executed only once when the class gets loaded into memory
- can have several in a class
- get executed in the order of their occurence
- cannot access non-static members

## Static Methods
- cannot access non-static members



## Examples
What is the output?
```java
class A {
    static {
        System.out.println("Static Block in A");
    }

    public static void display(String msg) {
        System.out.println(msg);
    }
}


class Main {
    public static int x = 1;

    static {
        System.out.println("Static Block in Main");

        public static void main(String[] args) {
            x++;
            A a = null;
            System.out.println("In main");
            a.display("x is: " + x);
        }
    }
}
```
Output is:
Static Block In Main
In main
Static Block in A
x is: 2

Reason:
-  `a.display(x);` is called on a `null` reference of class `A`. This works without throwing a `NullPointerException` because the display method in class `A` is a `static` method. 
- Java allows calling static mehtods using a reference variable as well, even if that reference variable is `null`, as the method call is resolved at compile time and does not depend on the instance existence at runtime
- it is not a good practice though, static method should be called on the class like `A.display()`

##### How to use Static members

- within same class: just use name of member
- in another class: use class name and then name of member using dot notation
- example:
  - Math.min(4, 5)
  - Math.PI
- one can call a static method using a reference variable but it is not a good practice, see above
