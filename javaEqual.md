composition, inheritance, java, equals, hashCode

# Overriding `equals()` and `hashCode()`

## `composition` over `inharitance` to fix `esquals()`

Implementation for the Object Class

`equals()`
The Object class defines both the equals() and hashCode() methods, which means that these two methods are implicitly defined in every Java class, including the ones we create:

```java
class Money {
    int amount;
    String currencyCode;
}
Money income = new Money(55, "USD");
Money expenses = new Money(55, "USD");
boolean balanced = income.equals(expenses)
```

We would expect income.equals(expenses) to return true, but with the Money class in its current form, it won't.

> The default implementation of equals() in the Object class says that equality is the same as object identity, and income and expenses are two distinct instances.

### Overriding equals()

Let's override the equals() method so that it doesn't consider only object identity, but also the value of the two relevant properties:

```java
@Override
public boolean equals(Object o) {
    if (o == this)
        return true;
    if (!(o instanceof Money))
        return false;
    Money other = (Money)o;
    boolean currencyCodeEquals = (this.currencyCode == null && other.currencyCode == null)
      || (this.currencyCode != null && this.currencyCode.equals(other.currencyCode));
    return this.amount == other.amount && currencyCodeEquals;
}
```

### equals() conditions

Java defines the conditions that our implementation of the equals() method must fulfill. The equals() method must be:

- reflexive: an object must equal itself
- symmetric: x.equals(y) must return the same result as y.equals(x)
- transitive: if x.equals(y) and y.equals(z), then also x.equals(z)
- consistent: the value of equals() should change only if a property that is contained in equals() changes (no randomness allowed)

### Violating equals() Symmetry With Inheritance

Violations happen most often if we extend a class that has overridden equals(). Let's consider a Voucher class that extends our Money class:

```java
class WrongVoucher extends Money {

  private String store;

  @Override
  public boolean equals(Object o) {
      if (o == this)
          return true;
      if (!(o instanceof WrongVoucher))
          return false;
      WrongVoucher other = (WrongVoucher)o;
      boolean currencyCodeEquals = (this.currencyCode == null && other.currencyCode == null)
        || (this.currencyCode != null && this.currencyCode.equals(other.currencyCode));
      boolean storeEquals = (this.store == null && other.store == null)
        || (this.store != null && this.store.equals(other.store));
      return this.amount == other.amount && currencyCodeEquals && storeEquals;
      }

  // other methods
  }
```

At first glance, the Voucher class and its override for equals() seem to be correct. And both equals() methods behave correctly as long as we compare Money to Money or Voucher to Voucher. But what happens, if we compare these two objects:

```java
Money cash = new Money(42, "USD");
WrongVoucher voucher = new WrongVoucher(42, "USD", "Amazon");

voucher.equals(cash) => false // As expected.
cash.equals(voucher) => true // That's wrong.
This violates the symmetry criteria of the equals() contract.
```

### Fixing equals() Symmetry With Composition

> To avoid this pitfall, we should favor composition over inheritance.

Instead of subclassing Money, let's create a Voucher class with a Money property:

```java
  class Voucher {

      private Money value;
      private String store;

      Voucher(int amount, String currencyCode, String store) {
          this.value = new Money(amount, currencyCode);
          this.store = store;
      }

      @Override
      public boolean equals(Object o) {
          if (o == this)
              return true;
          if (!(o instanceof Voucher))
              return false;
          Voucher other = (Voucher) o;
          boolean valueEquals = (this.value == null && other.value == null)
          || (this.value != null && this.value.equals(other.value));
          boolean storeEquals = (this.store == null && other.store == null)
        || (this.store != null && this.store.equals(other.store));
      return valueEquals && storeEquals;
      }

      // other methods
  }
```

Now equals will work symmetrically as required.

## `hashCode()`

`hashCode()`` returns an integer representing the current instance of the class. We should calculate this value consistent with the definition of equality for the class. Thus, if we override the equals() method, we also have to override hashCode().

### `hashCode()`` conditions

Java also defines a set of conditions for the hashCode() method.

- internal consistency: the value of hashCode() may only change if a property that is in equals() changes
- equals consistency: objects that are equal to each other must return the same hashCode
- collisions: unequal objects may have the same hashCode

### Violating the Consistency of hashCode() and equals()

The second criteria of the hashCode conditions has an important consequence: If we override equals(), we must also override hashCode(). This is by far the most widespread violation regarding the equals() and hashCode() methods contracts.

```java
class Team {

    String city;
    String department;

    @Override
    public final boolean equals(Object o) {
      // implementation
    }
}
```

The Team class overrides only equals(), but it still implicitly uses the default implementation of hashCode() as defined in the Object class. And this returns a different hashCode() for every instance of the class. This violates the second rule.

Now, if we create two Team objects, both with city “New York” and department “marketing,” they will be equal, but they'll return different hashCodes.

The trouble starts when some hash-based collections are involved. Let's try to use our Team class as a key of a HashMap:
```java`
Map<Team,String> leaders = new HashMap<>();
leaders.put(new Team("New York", "development"), "Anne");
leaders.put(new Team("Boston", "development"), "Brian");
leaders.put(new Team("Boston", "marketing"), "Charlie");

Team myTeam = new Team("New York", "development");
String myTeamLeader = leaders.get(myTeam);

````
We would expect myTeamLeader to return “Anne,” but with the current code, it doesn't.

If we want to use instances of the Team class as HashMap keys, we have to override the hashCode() method so that it adheres to the contract; equal objects return the same hashCode.
```java
@Override
public final int hashCode() {
    int result = 17;
    if (city != null) {
        result = 31 * result + city.hashCode();
    }
    if (department != null) {
        result = 31 * result + department.hashCode();
    }
    return result;
}
````

After this change, leaders.get(myTeam) returns “Anne” as expected.

### When Do We Override equals() and hashCode()?

- Generally, we want to ovrride either both of them or neither of them.

- Domain-Driven Design can help us decide circumstances when we should leave them be. For entity classes, for objects having an intrinsic identity, the default implementation often makes sense.

- For value objects, we usually prefer equality based on their properties. Thus, we want to override equals() and hashCode().
