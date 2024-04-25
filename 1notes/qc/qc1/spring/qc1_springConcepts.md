java, spring, bean

# [Spring](https://spring.io ) Concepts
Usually means the Spring Framwork.


## Spring Framework 

A Java framework used to develope Java applications.
It provides layers of abstraction in our Java Projects, primarily through Dependency Injection.

Why:
- lets the developer concentrate on writing business logic
- lets us write an appliction using POJOs (Plain Old Java Objects) while Spring is managing the infrastructure and applies services to our POJOs (no need for application server for example)

Advatages:
- Convention over Configuration
- use of POJOs
<br>Spring framework helps developers to develop enterprise applications using POJO. An enterprise container like an application server is not required while using POJOs.
- Flexibility for configuring Spring: 
    - XML or
    - Java-based annotations.
- No need for Server
<br>Spring framework provides a lightweight container and it can be activated without any web server or application server.
- No need for reinvention
<br>Spring uses technologies such as JDK timers, ORM frameworks, Java EE, etc. So developers need not have to learn all those technologies or frameworks to develop applications.
- Modularity
- Ease of Testability
<br>Spring Dependency Injection simplifies the injection of test data by using JavaBean POJO.
- Inversion Control and APIs
<br>Spring framework provides inversion control and APIs to translate exceptions thrown by JDBC and Hibernate into unchecked and consistent.


## Spring Modules 
Spring Modules are pieces of the Spring Framework. 

- Required Modules (needed for Spring to work as intended) 

    - `Core`
        - core functionality of Spring
        - BeanFactory interface

    - `Bean`
        - Bean configuration and functionality 

    - `Context`: 
        - ApplicationContext interface (the IoC container we use)

- Optional Modules  

    - `Spring Web/MVC`
        - functionality for handling HTTP requests
    - `SpringAOP` (Aspect Oriented Programming)
        - Handles “cross cutting concerns” like logging


![Spring Modules](image.png)

## Spring Projects
Spring Projects are built on Spring modules and provide solutions to issues faced by industry level applications. 

- think of them as add-ons
- are all open source
- `Spring Framework` is considered the foundational Spring Project (built on top of the Spring Core Module) 
- `Spring Boot` is considered a Spring Project too
- `SpringORM/SpringData: Two modules???????? that handle the application’s ORM (Object Relational Mapping) and the database connection. We’ll be using SpringData. 
- `Spring Security` 


## IoC: 

IoC is the act of taking control of some aspects of application away from the developer, and letting the Framework handle it instead. 

- the process of creating, initializing and managing the objects was initially a task for the developer, in Spring it is handled by Spring IoC through Dependency Injection


## Dependency Injection: 

 Injecting objects into other objects is called Dependency Injection.

 ### Types of Dependency Injections:
-  `Constructor Injection` 
    - uses a Class’s constructor
    - the injection happens at the Class instantiation. 
    - `

- `Setter Injection` - uses the setter method of a Class to add the dependencies slightly after instantiation (after the constructor is invoked) 

- `Field Injection`
    - inject dependencies in the variable declarations
    - bad practice !!!
    - breaks encapsulation


## Spring (IOC) Containers



 An object that creates (instantiates) and holds your Spring Beans, then injects them wherever they’re being called in the application. -nice QC line 

 Spring Container can be implemented in two different ways: 
 - BeanFactory
 - ApplicationContext

#### BeanFactory:  

- Older 
- Lazily instantiates beans. (Bean objects aren’t created until they’re needed) 
- Requires a resource object configuration, generally called the beans.xml to be instantiated. It’s super verbose and ugly. 

#### ApplicationContext:  
- Newer, it’s actually built on top of BeanFactory – it's an abstraction! 
- Eagerly instantiates beans (When the application starts, all the beans are ready) 
- Provides support for annotations (No longer have to do EVERYTHING in XML like we would have to if using BeanFactory) - The ApplicationContext can take XML configs directly for configuration 
```java
ApplicationContext ac = new
````



## Spring Beans

Java Classes managed by the Spring  to be used for dependency injections.


### How to define a Bean


#### 1. with Stereotype annotations
- are used to create beans automatically in the application context
- types:
    - `@Component` - most common: generic annotation to make a class a bean
    - `@Repository` - used for DAO classes
    - `@Service` - used for service classes
    - `@Controller` - used for controller classes
#### 2. Configuration Java Class
#### 3. XML Configuration
- via the `<bean>` tag


## Bean Wiring

Bean Wiring is how we connect our beans as dependencies of one another.

- When you need to access an other class's method like a Service Class calls a DAO Class method, you use dependecy injection to establish a connection between them.
- Types
    - Constructor Injection
    - Setter Injection
    - Field Injection (DO NOT USE)

 
#### Autowiring: 
A process that “Automagically” determines the dependencies for you, and then provides them. 

 - automagically means that @Autowired will abstract away the dependency injection that it does for you. So to us, it looks automatic and magical  

- There are two ways to use autowiring: 

    - XML (won’t see this after HelloSpring) 

    - Annotation-Driven 

- usege: put the `@Autowired` annotation above a constructor, or setter, depending on what type of injection you want



 
 

### Bean Lifecycle (QC loves to ask, I’m sorry) 
![alt text](image-3.png)

1. Setup
- Spring IOC starts
- Bean Instantiated
- Dependencies Injected
- Internal Spring processing
- Custom init method( ready for use)
2. Bean is ready for Use
3. Bean is ready for garbage collection
- Container shutdown
- Custom destroy method


 

## Bean Scopes: 

 Bean Scope refers to how many instances of a Bean are/can be created and where they are used. (QC Line) 

### Types:
- Universal Scopes
    - Singleton
        - the container creates a single instance of that bean
        - the default Scope
        - to define it explicitly use: `@Scope("singleton")`
    - Prototype
        - will return a different instance every time it is requested from the container
        - `@Scope("prototype")` 
- Web Aware Scopes (for Application that can take HTTP requests)
    - Request - creates a Bean for an HTTP Request
    - Session - creates a Bean for an HTTP Session
    - Application - creates a Bean for a ServletContext
    - WebSocket - creates a Bean for a WebSocket session


## Spring Annotations:
### Spring Core Annotations



################ QUESTIONS BELOW ########################
## Spring Concept Questions


### Spring General Questions

>What is it? 

>What does it do for us?   

>How do we build a spring application? 

### IoC questions

>What is Inversion of Control? 

>What control does Spring invert exactly? 

>What does the phrase convention over configuration mean in Spring? 

>Benefits and drawbacks of Spring’s opinionated tendencies? 


### Dependency Injection Question

>What is it? 

>What are the types? 

>What does Spring use? 

>Why is field injection bad? (Breaks encapsulation - ignores OOP getters/setters/private) 

### Spring IoC Container Questions
>What are they? 

>What are your two options? (BF vs AC) 

>What’s the difference between them?  

>Which one do we use? 

>How do I build and access a Spring Container?  

### Bean Scope Questiona:
> What are they?

> Which ones are common to all Spring applications? (two of them)

> Know the difference between singleton and prototype scopes

>Which ones are web aware? (four of them)



>Stereotype Annotations: 

> - What do they do? 

>- Why are they called that? 

>- What are the 4 annotations? 

 

### Bean Wiring Questions 

>What is it?  

>Why do we do it? 

>What are the three ways we can do it? (XML, Class-based, Annotation-driven) 

>Which way is the best/easiest? 

>What does “automagically” mean?  


 

### Bean Lifecycle Questions: 

>Know it conceptually 

>Know the 8 steps of the setup and teardown process. (You don’t have to memorize the steps that are italicized.) 

