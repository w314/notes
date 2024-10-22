# Interface vs Abstract Class

<table>
<tr>
<th>Feature</th>	<th>Interface</th><th>Abstract Class</th>
</tr>
<tr>
<td>Methods</td>
<td>Can have abstract, default, and static methods</td><td>Can have abstract and concrete methods</td></tr>
<tr>
<td>Fields</td>	<td>Can have only static final fields (constants)</td>	<td>Can have instance fields (state)</td></tr>
<tr><td>
Multiple Inheritance</td>	<td>A class can implement multiple interfaces</td>	<td>A class can extend only one abstract class</td></tr>
<tr><td>
Constructors</td>	<td>Cannot have constructors</td>	<td>Can have constructors</td></tr>
<tr><td>
Inheritance</td>	<td>Used to define a contract for behavior</td>	<td>Used to define a base class with common behavior and state</td></tr>
<tr><td>
State</td>	<td>Cannot maintain state</td>	<td>Can maintain state</td></tr>
</table>

## Interface

```java
public interface Animal {
    void eat(); // Abstract method
    void sleep(); // Abstract method

    default void breathe() {
        System.out.println("Breathing...");
    }

    static void info() {
        System.out.println("This is an Animal interface.");
    }
}
```
- `default method`
    - provides a default implementation
    - can be overridden by implementing class
- `abstract method`
    - without method body
    - must be implemented by implementing classes
- `static method`
    - has method body
    - 