aop

 

# Aspect Oriented Programming

 

> `Cross-Cutting Concerns` are functionalities common to all layers like logging, security and transaction management.

 

> `Aspect Oriented Programming (AOP)` provides a way to separate cross-cuttin conerns from business logic code.

 

- creates loosely coupled application

- uses `AspectJ`, a popular AOP Framework

 

## Elements of AOP

 

### Aspect

 

>`Aspect` is a class that implements the cross-cutting concerns.

 

- class should be annotated with `@Aspect`

- use with classes that are annotated with `@Component` or its derivatives

 

### Join Point

> A `Join Point` is a specific point in the application. In Spring AOC it is alwasy the exectuion of a method.

 

Join Point in general can be:

- method execution

- exception handling

- object variable value change

- etc

 

### Advice

> `Advice` is a method of the `Aspect Class`, it provedies the implementation of the cross-cutting concern.

 

It gets executed at the selected join point.

 

Advice Types:

- `Before` executed before join-point

- `After Returning` executed after execution of join-point finishes

- `After Throwing` executed if any exception is thrown from the join-point

- `After (Finally)` executed after execution of join-point in any case

- `Around` invoked before AND after join point execution

 

Examples:

```java

@AfterReturning("execution(* com.wp.service.*Impl.*(..))")

public void afterReturning() MyException {

    LOGGER.info("After returning advice called.");

}

 

// to access the value return by the jointpoint:

// value of returning has to = parameter of cross-cutting method (both are returnValue)

@AfterReturning(value = "execution(* com.wp.service.*Impl.*(..)),returning = "returnValue"")

public void afterReturning(String returnValue) throws MyException {

    LOGGER.info("After returning advice called.");

}

 

// use the throwing attribute to access the exception thrown from target method

// make sure variable name matches with parameter used in function (exception in this case)

@AfterThrowing(pointcut = "execution(* com.wp.service.*Impl.*(..))", throwing = "exception")

public void afterThrowing(MyException exception) throws MyException {

    LOGGER.error(exception.getMessage(), exception);

}
```
 

### Pointcut

> `Pointcut` represents an expression used to identify a join-point.

 

`Pointcut Expression` examplej:

```java

execution(<modifiers> <return-type> <fully qualified class name>.<method-name>(parameters))

```

- `execution` is a keyword called the `pointcut designator`

- `<modifier>` is optional can be

    - public

    - protected

    - private

- `<return-type>` is mandatory, determines the return type of them method to match the join point, if it does not matter `*` can be used

- `<fully qualified class name>` is optional, determines the name of the class(es) which has methods that the advice executed on, `*` can be used for the name or part of the name

- `<method name>` is the name of the method on which the advice is executed, `*` can be used as a name or part of the nem

- `parameters` are used to matching parameters. to skip parameter filtering use `..` as parameters

 

Examples:

`execution(public * *(..))`

execution of any public method

 

`execution(* service*(..))`

execution of any method with a name beginning with “service”

 

`execution(* com.wp.service.*.*(..))`  

execution of any method defined in the com.wp.service package

 

`execution(* com.wp.service.CustomerServiceImpl.*(..))`

execution of any method defined in CustomerServiceImpl of com.wp.service package

 

`execution(public String com.wp.repository.CustomerRepository.*(..))`

execution of all public method in CustomerRepository of com.wp.repository package that returns a String

 

## How to use Spring AOP

 

### Add dependency

 

`pom.xml`

```java

<dependency>

    <groupId>org.springframework.boot</groupId>

    <artifactId>spring-boot-starter-aop</artifactId>

</dependency>

```

 

### Add Advises to Classes

- annotate class with `@Aspect`

- add Advises with type `@Before` and `PointCut`

```java

@Component

@Aspect

public class LoggingAspect {

 

    public static final Logger LOGGER =

            LogManager.getLogger(LoggingAspect.class);

 

    // Will log before any method executio in the package marked in pointcut        

    @Before("execution(* com.wp.service.*Impl.*(..))")

    public void before() throws InfyBankException {

        LOGGER.info("Before advice called.");

    }

//....

```

