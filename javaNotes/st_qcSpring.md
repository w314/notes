java, spring, bean

# Spring: 

## Spring Framework 

>What is it? 

>What does it do for us?   

>How do we build a spring application? 

Terms:  

Spring Bean 

Spring/IoC Container 

Spring Module 

Know the required ones and some optional ones 

Spring Project 

Bean Wiring 

 

## IoC: 

What is Inversion of Control? 

What control does Spring invert exactly? 

What does the phrase convention over configuration mean in Spring? 

Benefits and drawbacks of Spring’s opinionated tendencies? 

 

## Dependency Injection: 

What is it? 

What are the types? 

What does Spring use? 

Why is field injection bad? (Breaks encapsulation - ignores OOP getters/setters/private) 

 

## Spring Containers: 

What are they? 

What are your two options? (BF vs AC) 

What’s the difference between them?  

Which one do we use? 

How do I build and access a Spring Container?  

 

## Stereotype Annotations: 

What do they do? 

Why are they called that? 

What are the 4 annotations? 

 

## Bean Lifecycle: 

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

