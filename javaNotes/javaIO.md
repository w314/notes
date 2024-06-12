
# Input - Output

## Input
### Scanner class

> What is the Scanner class used for? Give an example of how you would use it.

The `Scanner` class is used to get user input.

- needs `import java.util.Scanner;`


```java

// create Scanner object
Scanner myScanner = new Scanner(System.in);

// prompt user for input
System.out.println("Enter username:");

// read and store user input
int userAge = myScanner.nextInt();
// consume hidden newLine character
myScanner.nextLine();


// read until end of input
while( myScanner.hasNext()) {

}
// can by used with .hasNextInt() etc


// close sanner
myScanner.close()
```

Methods:

- `nextBoolean()` Reads a boolean value from the user
- `nextByte()` Reads a byte value from the user
- `nextDouble()` Reads a double value from the user
- `nextFloat()` Reads a float value from the user
- `nextInt()` Reads a int value from the user
- `nextLine()`
  - Reads a String value from the user
  - OR used to consume hidden newline character (between calling two nextInt() for example)
- `nextLong()` Reads a long value from the user
- `nextShort()` Reads a short value from the user

If you enter wrong input (e.g. text in a numerical input), you will get an exception/error message (like `InputMismatchException`).

## Output

## printf()

```java
System.out.printf(format, arguments);
System.out.printf(locale, format, arguments);
```
- rules start with `%`
- `%[flags][width][.precision]conversion-character`
    -  


### Number formatting
```java
int a=10000; 
            
//System.out.printf("%.d%n",a); 
System.out.printf("%,d%n",a); 


 double a = 3.14159265359; 
  
        // Printing Double Value with 
        // different Formatting 
        System.out.printf("%f\n", a); 
        // 3.141593
        
        System.out.printf("%5.3f\n", a); 
        // 3.142
        
        System.out.printf("%5.2f\n", a); 
        //  3.14
```

#### Print Statements
