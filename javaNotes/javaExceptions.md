java, exceptions, try, catch, try-catch

# Java Exception Handling


## Examples

What is the output of the following code:
```java
class StringOperator {
    String value;

    public void modifyString(String value) {
        int len = value.length();
        try {
            throw new Exception("Exception in modifier");
        } catch(Exception e) {
            System.out.println("Caught in modifier " + e.getMessage());
        } finally {
            System.out.println("No more exception in modifier");
        }
        System.out.println("Modify completed");
    }
}


class Main {
    public static void main(String[] args) {
        try {
            new StringOperator().modifyString("Exceptions");
        } catch(Exception e) {
            System.out.println("Caught in main " + e.getMessage());
        } finally {
            System.out.println("No more exceptions in main");
        }
    }
}
```
Caught in modifier Exception in modifier
<br>No more exception in modifier
<br>Modify completed
<br>No more exceptions in main

