java, inheritance

# Java Inheritance
- NO multipel inheritance in Java
- What is inherited?
    - all non-private methods
    - all non-private attributes

- Uses the `extends` keyword
- `final` classes cannot be extended
- identifiers use PascalCase

```java
class Customer {}

class RegularCustomer extends Customer {}
```

## Constructor call in inheritance
- when a child class object is created with `new`
- the sequence of constructor invocation
    - child class constructor is invoked
    - child class constructor first invokes parent class constructor
    - only after that executes statements in its own constructor
```java
class Customer {
	public Customer() {
		// 3: Parent constructor will be executed
		System.out.println("Creating a customer...");
		// 4: The flow will go back to the child constructor
	}
}
class RegularCustomer extends Customer {
	public RegularCustomer() {
		// 2: This constructor will then call the parent constructor
		System.out.println("It is a regular customer!");
		// 5: The flow will finally come here
	}
}
public class Tester {
	public static void main(String[] args) {
		RegularCustomer regularCustomer = new RegularCustomer();
		// 1: This line will be executed first and the flow will go to [2]
	}
}
```

## `super` keyword

`super()` invokes the parent class's constructor

```java
public RegularCustomer(String custId, String custName) {
		super(custId,custName);    //Invoking the parent class parameterized constructor
		this.discount = 5.0f;
		System.out.println("Child Constructor");
}
```


## `sealed` classes
- Java 15 onwards
- helps to prevent unauthorized class extensions
- subclasses of a `sealed` class  does NOT have to `final`, but can be `non-sealed`
- in building the class hierarcy
    - `sealed` classes allow control
    -  `non-sealed` classes allow flexibility
```java
// CLASS HIERARCHY EXAMPLE
public sealed class Customer permits RegularCustomer, CorporateCustomer {}

final class RegularCustomer extends Custemer{}

non-sealed class CoprorateCustomer extends Customer{}

final class PremiumCustomer extends CorparetCustomer{}

// CLASS HIERARCHY EXAMPLE
sealed class Account permits SavingsAccount{}

sealed class SavingsAccount extends Account permits StudentAccount{}

final class StudentAccount extends SavingsAccount{}
```

## Type Checking

To use Customer methods on person we have to be sure person is a Customer.

traditional syntax
```java
if(person instanceOf Customer) {
    Customer customer = (Customer) person;
}
```

### Pattern matching
- introduced in Java 16
```java
if (referenceName instanceof ClassName instanceName) {
} else {
}
```
- refrenceName - object you want to check the type of (person)
- ClassName - desired type you want to match against (Customer)
- instanceName - the name of the new variable that will be created and assigned the value of referencname if it mathes the typ

```java

// function checks the type of employee and class the dipslay function of the appropriate matching class
private static void checkType (Employee employee) {
      if (employee instanceof PermanentEmployee permanent) {
    // call display function of permanent employee
            permanent.displayPermanentEmployee;
      }
      else if (employee  instanceof PartTimeEmployee partTime) {
            partTime.displayPartTimeEmployee();
      }
      else {
            System.out.println("No instance found");
      }
}
```
