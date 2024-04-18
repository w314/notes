
# Spring Boot: 
Spring Boot is a **Spring Project** used to create standalone Spring-based applications that you can "just run".

Spring Boot is a tool that makes developing a web application and microservices with Spring Framework faster and easier through:
- Autoconfiguration
- An opinionated approach to configuration
- The ability to create standalone applications

### Features of spring boot?
- In-built starter projects.
- In-built WebServers.
- RestTemplate supports.
- JSON Support.
- Third-Party Integration Support.

### Why Spring Boot over Spring?
- Actuators.
- Version Management.
- Auto Configuration.
- Component Scanning.
- Embedded server (Tomcat).
- InMemory DB.
- Starter POM.

## Spring Boot Questions

> What is it? (Opinionated autoconfiguration of Spring) 

> What are some benefits/advantages of Spring Boot? 

> How do you implement it?  

>Know about the embedded tomcat server.  

>Know what opinionated means 

>Know the annotations in the main method class to run a Spring Boot app.  

>Know what Spring Boot Actuator and DevTools do 

>What is the Spring environment Interface? What does it allow us to do? 

>Properties? 

>Profiles? 

>What is validation? (Check revpro notes) 



# Spring MVC (aka Spring Web)

Spring MVC is used to implement the Model-View-Controller architecture.

 MVC Architecture
- Model - data related
- View - ui related
- Controller - business logic, interface between Model and View

Spring MVC
- provides a front controller named `DispatcherServlet`, which handles all the requests and responses.
- all the controllers are annotated with `@Controller` and are managed by DispacherServlet.
- a spring MVC configuration file is created to manage the controllers.
- the requests from the client is taken by web.xml and sent to the DispatcherServlet and based on the request the respective controller is called.
- the response from the controller is a model and view name. TODO????
 - the DispatcherServlet communicates with the view template.



In Spring Boot you need the `WEB` dependency
```bash
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
```

## Sprign MVC Questions 
>What is it? 


>What does MVC stand for?

Model - View - Controller 
>What does it do for us?  

>What is its structure? What do the following classes/interfaces do: 
    > -  DispatcherServlet 
    >- HandlerMapping/RequestMappingHandlerMapping 
    >- ViewResolver 
    >- ContextLoaderListener 

>Know the SpringMVC application flow.  

>What is a Controller? 

>When are they Controllers called, and by what? 

>Know the annotations and what they do (annotations cheat sheet in the notes should be helpful) 

>Look into @RequestParam in the curriculum, just in case it’s asked 

>What is RestTemplate? What does it let us do? 


# Spring Data JPA

## Spring Data JPA Questions 

>What is the JPA? What does it let us do? 

>What are some annotations we use from JPA? Where do we use them? 

>What does ORM stand for? 

>What benefits does Spring Data provide? 

>What is the interface hierarchy? 

>Which interface do we implement to make our custom DAOs? 

>We can’t instantiate interfaces... how do we use the methods in our custom DAOs? 

>Know the Spring Data annotations 

>Know @Transactional annotation and what a transaction is. 

>Look into the transaction propagation strategies in revpro 

>Look at the ACID properties, memorize the main rule for each property.  

 

 

## Lombok 

### Lombok Questions
>What is it? How do we implement it? 

>How does it help us? 

>What is the drawback of Lombok that Ben mentioned? 

