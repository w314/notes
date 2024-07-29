java, exceptions, try, catch, try-catch, error

# Java Errors & Exceptions Handling

> What is the difference between an Error and an Exception?

Both `Error` and `Exception` extend the `Throwable` class

### `Error`

- `Compilation Error`

  - occurs at compile time
  - syntax error
  - not handling checked exceptions
  - eg: `SyntaxError`

- `Runtime Error`

  - occurs at runtime
  - severe problem with the program
  - we dot hand attempt to recover from them
  - eg: `OutOfMemoryError`

### `Exception`

Exceptions are the conditions that occur at runtime and may cause the termination of the program. But they are recoverable using try, catch and throw keywords.

#### Exception Handling

> How would you handle an exception?

Exception can be recovered from with `try - catch`:

- checked
  - must be handled
  - eg: `IOException`
- unchecked
  - runtime errors
  - eg: `ArrayOutOfBounds`

When risky code is written that has the possibility of throwing an exception, it can be dealt with in one of two ways:

1. `Handling` means that the risky code is placed inside a `try/catch` block
2. `Declaring` means that the type of exception to be thrown is listed in the method signature with the throws keyword. This is also called "ducking" the exception - you let the code which calls the method deal with it.

If the exception is not handled anywhere in the program, it will propagate up through the call stack until it is handled by the JVM which then terminates the program.

> What is the difference between a checked and an unchecked exception?

- Checked exception require mandatory handling:

  - try - catch
  - throws

- Handling the exception is checked during compilation, gives compliation error if not handled.

- Exception-handling is mandatory for any exception class that is not a subclass of either Error or RuntimeException.

#### Creating Custom Exceptions

- A programmer can create custom exceptions in Java by extending any exception class.
- If you extend RuntimeException, however, you will be creating an unchecked exception.
  - This is a good idea if you do not want other code to have to handle your exception being thrown.
  - If you do always want to require your exception to be handled, then create a checked exception by extending any existing one, or the Exception class itself.

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

