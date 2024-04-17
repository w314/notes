java, spring, bean

# [Spring](https://spring.io ) 
Usually means the Spring Framwork.
## Spring Framework 

>What is it? 

>What does it do for us?   

>How do we build a spring application? 

A standalone open-source framework developed to suppert the development of enterprise scale applications.

- makes development easier.
- provides layers of abstraction through dependency injection


## Quick Terminology  

### Spring Bean 
A class registered with the Spring Container

- they can be injected as a dependency

### Spring/IoC Container 
 An object that creates (instantiates) and holds your Spring Beans, then injects them wherever they’re being called in the application.
### Spring Module 
Parts of the Spring FrameWork
- required 
- optional


Know the required ones and some optional ones 
### Spring Project 
Optional extention to the Spring Framwork.

### Bean Wiring 
 Configuration on how our beans are connected to each other. This is how we tell Spring where and how to inject our beans as dependencies. 
 

## IoC: 
>What is Inversion of Control? 

>What control does Spring invert exactly? 

>What does the phrase convention over configuration mean in Spring? 

>Benefits and drawbacks of Spring’s opinionated tendencies? 

IoC is the act of taking control of some aspects of application away from the developer, and letting the Framework handle it instead. (The CONTROL of the application development is being INVERTED away from the programmer.) 

In Spring’s case this is done through dependency injection.  

## Dependency Injection: 

>What is it? 

>What are the types? 

>What does Spring use? 

>Why is field injection bad? (Breaks encapsulation - ignores OOP getters/setters/private) 

 Injecting objects into other objects is called Dependency Injection.

 ### Dependency Injection Types:
-  `Constructor Injection` - This sets dependencies using a Class’s constructor so that the injection happens at the same time as Class instantiation. 

- `Setter Injection` - uses the setter method of a Class to add the dependencies slightly after instantiation (after the constructor is invoked) 

- `Field Injection`
    - inject dependencies in the variable declarations
    - bad practice !!!
    - breaks encapsulation


## Spring Beans

Java Classes managed by the Spring  to be used for dependency injections.

### How to define a Bean


>Stereotype Annotations: 

>What do they do? 

>Why are they called that? 

>What are the 4 annotations? 
#### 1. Annotation Driven - with stereotype annotations
- `@Component` - generic annotation to make a class a bean
- `@Repository` - used for DAO classes
- `@Service` - used for service classes
- `@Controller` - used for controller classes
#### 2. Configuration Java Class
#### 3. XML Configuration
- via the <bean> tag


## Spring (IOC) Containers

>What are they? 

>What are your two options? (BF vs AC) 

>What’s the difference between them?  

>Which one do we use? 

>How do I build and access a Spring Container?  

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
 

### Bean Lifecycle: 

Know it conceptually 

Know the 8 steps of the setup and teardown process. (You don’t have to memorize the steps that are italicized.) 

 

## Bean Scopes: 

What are they?  

Which ones are common to all Spring applications? (two of them) 

Know the difference between singleton and prototype scopes 

Which ones are web aware? (four of them) 

 

## Bean Wiring: 

What is it?  

Why do we do it? 

What are the three ways we can do it? (XML, Class-based, Annotation-driven) 

Which way is the best/easiest? 

What does “automagically” mean?  

 

## SpringMVC:  

What is it? 

What does MVC stand for? 

What does it do for us?  

What is its structure? What do the following classes/interfaces do: 

DispatcherServlet 

HandlerMapping/RequestMappingHandlerMapping 

ViewResolver 

ContextLoaderListener 

Know the SpringMVC application flow.  

What is a Controller? 

When are they called, and by what? 

Know the annotations and what they do (annotations cheat sheet in the notes should be helpful) 

Look into @RequestParam in the curriculum, just in case it’s asked 

What is RestTemplate? What does it let us do? 

 

 

## Spring Data JPA: 

What is the JPA? What does it let us do? 

What are some annotations we use from JPA? Where do we use them? 

What does ORM stand for? 

What benefits does Spring Data provide? 

What is the interface hierarchy? 

Which interface do we implement to make our custom DAOs? 

We can’t instantiate interfaces... how do we use the methods in our custom DAOs? 

Know the Spring Data annotations 

Know @Transactional annotation and what a transaction is. 

Look into the transaction propagation strategies in revpro 

Look at the ACID properties, memorize the main rule for each property.  

 

## Spring Boot: 

What is it? (Opinionated autoconfiguration of Spring) 

What are some benefits/advantages of Spring Boot? 

How do you implement it?  

Know about the embedded tomcat server.  

Know what opinionated means 

Know the annotations in the main method class to run a Spring Boot app.  

Know what Spring Boot Actuator and DevTools do 

What is the Spring environment Interface? What does it allow us to do? 

Properties? 

Profiles? 

What is validation? (Check revpro notes) 

 

## Lombok 

What is it? How do we implement it? 

How does it help us? 

What is the drawback of Lombok that Ben mentioned? 

