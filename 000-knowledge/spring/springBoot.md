
# Spring Boot: 
Spring Boot is a **Spring Project** used to create standalone Spring-based applications that you can "just run".


WHy SPring BOOt
- embedded tomcat
- intializer
- no xml configuration
- provides dependencies at initalization
- creates standalone applications (that just run)
- convention over configuration


- actuator si a dependency
- devtool is a dependecy


Spring Boot is a tool that makes developing a web application and microservices with Spring Framework faster and easier through:
- Autoconfiguration
- An opinionated approach to configuration
- The ability to create standalone applications


Creates our ApplicationCOntext.xml for us



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


### Spring Boot Environment

Spring Boot allows to externalize configuration so we can work with the same application code in different environments. 

#### Ways to externalize configuration
- property files
- YAML files
- environment variables
- command line arguments


Examples:
```java
// using property files
@Configuration
@PropertySource("classpath:application.properties")
// same but with using a placholder for an environment variables
@PropertySource("classpath:persistence-${envTarget:mysql}.properties")
public calss MyClass {}


// injecting a property with teh @Value notation
@Value(${jdbc.url})
private String jdbcUrl;
```

### Parent Child Context
The properties file can be defined in the Parent or Child context, based on if it is defined in:

- Parent context
    - @Value
        - works both in parent and child
    - environment.getProperty()
        - works both in parent and child
- Child context
    - @Value
        - only works in child context
    - environment.getProperty()
        - only works in child context


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



 

## Lombok 

`Lombok` is a Spring Project designed to remove the need to write repetitive boilerplate code for our Classes (typically the models). 

Lombok lets you use annotations to determine what boilerplate code you want the framework to include in our Java objects. The code is then inserted for you at compile time.  

### Lombok Annotations 

- @Getter 

- @Setter 

- @NoArgsConstructor 

- @AllArgsConstructor 

- @ToString 

- @EqualsAndHashCode 

- @Data 
- and others... 

### Lombok installation: 

For your IDE to work well with Lombok, it must be installed in the IDE. Otherwise, it will not be aware of the methods that Lombok is providing.  

### How to use Lombok
```java
@Entity
@Table(name = "books")
@Data // Lombok annotation to generate getters, setters, hashCode and toString methods
@NoArgsConstructor // Lombok annotation to generate no args constructor
@AllArgsConstructor // Lombok annotation to generate all args constructor
public Books {

}
```
Why might Lombok not be a good choice? 

If you’re working on a personal project that only you (or maybe a couple others) will use, it’s probably fine 

The problem arises when many people are intended to clone the application or develop it alongside you. By implementing Lombok, you force other developers working on your project to use it too. 

 
## Lombok Questions
>What is it? How do we implement it? 

>How does it help us? 

>What is the drawback of Lombok that Ben mentioned? 

