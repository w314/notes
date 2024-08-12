java, lambda, funtional interface, method-reference

# Lambda Expression
>`Lambda Expressions` area  type of `Functional Interface` (Interface with only 1 abstract method), where they follow the definition of the `Abstract Functional Method` of the interface.

- anonymus method. 
- enables a method to be passed as an argument to other methods as and when required.
- functional programming feature in Java
- syntax `( arugments ) -> { body }`
- `->` is the `Lambda Operator`

Example
```java
@FunctionalInterface
interface Operation{
	//Abstract Functional Method providing definition of lambda expression
	public double calculations(double num1,double num2); 
}
//Defining a lambda expression of type Operation
Operation doAdd  =  (double x, double y)-> x+y;
```


Possible Lambda Expression Syntaxes:
```java
() -> System.out.println("No Arguments passed in this Lambda Expression")

//For single parameter () is optional and declaration of type is optional
/*
 * Note:
 * For body consisting only 1 statement, {} is not necessary and
 * Return keyword must not be used for returning values!
 */
num -> num+100                                         

//If the data type of the single argument has to be declared, then the use of () is compulsory!!!!
/**
 * Note:
 * For body consisting more than 1 statements, {} is needed 
 * Return keyword is required to be used if any value is to be returned
 */
(double rate) -> { rate = rate*100;                                   
System.out.println("One argument passed: " +rate);
}


//For multiple arguments, declaration is optional only when all arguments are of same type
//Also the use of () is mandatory when declaring multiple arguments!!!
(num1, num2, num3) -> System.out.println("Multiple arguments passed: " +num1+","+num2+","+num3)

(int num1, int num2, String result) -> {
if(num1 + num2 > 100)
    result="Pass";
else
    result="Fail";
return result;
}
```

Calculator using java expressions example:
```java
interface Operation {
	public double opCriteria(double firstNum, double secondNum);
}

public static void main(String[] args) {
		
	Operation add = (x,y) -> x+y;
	Operation subtract = (x,y) -> x-y;
	Operation multiply = (x,y) -> x*y;
	Operation divide = (x,y) -> x/y;
		
	
	System.out.println("Result is: "+doOperation(12, 4, multiply));
}

public static double doOperation(double firstNum, double secondNum, Operation operator) {
	return operator.opCriteria(firstNum, secondNum);
}
```

# Method Reference
> Alternative to lambda expressions where the lambda expressions calls an existing method.

- Syntax: `ClassName::methodName`
- more concise and succinct
- does not support passing arguments

```java
List<String> strArr = List.of("Tyson", "Kai", "Max", "Ray", "Daichi");

//Printing List Using Lambda Expression
strArr.forEach(s -> System.out.println(s)); 

//Printing List Using Method Reference 
strArr.forEach(System.out::println);                                   
```

