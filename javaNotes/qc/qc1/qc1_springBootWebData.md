
# Spring Boot: 
Spring Boot is a **Spring Project** used to create standalone Spring-based applications that you can "just run".


WHy SPring BOOt
- embedded tomcat
- intializer
- no xml configuration
- provides dependencies

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

Spring MVC is a module of the Spring Framework used to implement the Model-View-Controller architecture.

MVC Architecture
- Model - data related
- View - ui related
- Controller - business logic, interface between Model and View

## Spring MV Structure

![Spring MV Structure](image-2.png)


`DispatcherServlet`
- a Front Controller that which handles all the requests and responses (handles all HTTP traffic)

`HandlerMapping`
- an Interface that is responsible for sending requests to the proper controllers 
- tells the DispatcherServlet which controller takes which HTTP Request.  
- the most common implementation is the RequestMappingHandlerMapping which is what we’ll use (see @RequstMapping below)???????

`Controllers`
- are annotated with `@Controller` and are managed by DispacherServlet
    - stereotype annotation (makes a class a bean)
    - with more functionality in Spring MVC
    - in Spring MVC it indicates the class will handle HTTP requests
- `@RequestMapping`: This annotation in a `@Controller` Class specifies what URIs (endpoints) the controller will handle. It can be placed before the Class declaration or above a method declaration. 
- there are also `@___Mapping` (@GetMapping, @PostMapping) for methods within a Controller that specify what verbed requests go to that certain method
- the `ResponseEntity` object is used to send back responses to the client. It lets us set status code and the body of the response.  

`ContextLoaderListener` - This automates the creation of our ApplicationContext for us so that our application and its server can “just run”

## Spring MVC Application FLow
- When the `Tomcat server` receives a `HTTP request`, it gets passed to the `DispatcherServlet` (our Front Controller) 

- The `DispatcherServlet` consults the `HandlerMapping`(which looks for `@RequestMapping` annotations) to determine which controller to send the request to, based on the `URI` (the /endpoint) of the HTTP request. 

- The controller layer consults the service/business logic layer to process the request 

- (service, dao, and DB do their thing) 

- The controller builds the response, and hands it back to the DispatcherServlet 

- The DispatcherServlet then consults the ViewResolver if necessary to process a view (which we won’t use, since we will have our own frontend views) 

- The DispatcherServlet hands the response back to the Tomcat Server, which sends it to the front end (or wherever the request came from, like postman maybe) 

- The HTTP lifecycle starts again whenever a new request is sent! 
 
### Spring MVC Annotations
- `@RequestMapping`
    - is a class and method level annotation used to map web requests to spring controller methods
 ```java
 @RequestMapping(value ="/submit", method = RequestMethod.POST)
//  OR
@PostMapping("/users")
@GetMapping("/users")
@DeleteMapping("/users/{userId}")
// and so on
 ```

- `@PathVariable`
    - extracts values from the request URI **path**
    - not encoded
- `@RequestParam`
    - extract values form the request URI **query string**
    - encoded

## Sprign MVC Questions 
>What is it? 

Spring MVC is a module of the Spring Framework used to implement the Model-View-Controller architecture.

>What does MVC stand for?

MVC Architecture
- Model - data related
- View - ui related
- Controller - business logic, interface between Model and View

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


# Spring Data JPA (Java Persistence API)  


## Spring Data
- is a Spring Project 
- Spring Data provides Abstractions/interfaces you can use based on the type of database (relational or non-relational)


### Spring Data Interface Hierarchy

This is the inheritance hierarchy for Spring Data’s interfaces used to create your DAO classes

 - `Repository`
    - base class for all the repositories providing access to databases

- `CrudRepository`
    -  extends Repository
    - it provides CRUD operations irrespective of databases
- ... many other

- `JpaRepository`
    - extends several interface
    - contains most of the basic DAO methods you’ll want to use.
- Your Custom Interface
    - all our DAOs extend JpaRepository


## Spring Data JPA (Java Persistent API) 
- is a Spring Data module
- works with relational databases
- defined in the `javax.persistence` package
- uses the `EntityManager Interface` to do CRUD operations in the database
- has standardized annotations to map our Java models to Database tables
- uses `JDBC` under the hood
- abstract away from the `Hibernate` framework
- uses ORM framework

### Advanteges over JDBC
- simpler
-  easier to change our database dialect, we just change the config file *application.properties*
- converts the ResultSet automatically to POJOs
- no need to know table specific knowledge (table and column names)
- needs  MUCH less lines of connection code and DAO code


### JPA Annotations

#### Fundamental JPA Annotations
(Definitely on QC) 

- used for entity mapping/configuration in our Java Classes
- `Entity mapping` means mapping our Java Classes into DB ENTITIES.


##### Mapping Tables

`@Entity`
- indicates that the Class is meant to be mapped to a DB table 

`@Table` 
- used for setting table options such as the name of the table in the database 

- doesn’t actually make a class a table (@Entity does that)

##### Mapping Table Columns
`@Column` 
- Hibernate will turn all of a Class’s field in DB columns by default
- BUT using the annotation lets us set things such as column name, or constraints like not null, and unique.   


##### Mapping Primary Keys
The 2 below would define an autogenerated primary key:

`@Id` - Declares a variable as a primary key in a table 

`@GeneratedValue`
- gives you control over the options for how Hibernate will auto-generate your primary key 
```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private int gameId;
```
 
#### JPA Relationship Annotations 

`@ManyToOne`/`@OneToMany`/`@ManyToMany` 
- define the relationship between our model classes in Java. (Which, as we know, map to tables in our DB.) 

The relationship is defined from the perspective of the Class in which the annotation sits. 
- the field on the “Many” side would have @ManyToOne
- field on the “One” side would have @OneToMany
- enough to annotate just the @ManyToOne side

In these relationship annotations, we can specify a few attributes, like CascadeType and FetchType (read below) 

@JoinColumn - Specifies a column to establish the relationship on. Just like we do normally, this is usually a Foreign Key pointing to the Primary Key of the table being referred to.  

CascadeType specifies the cascading on the database when removing/updating items. This is how we maintain referential integrity in hibernate. 

I tend to always use CascadeType.ALL when possible, making all typical Cascade operations occur when needed.  

FetchType determines if the related objects are called from the database immediately (EAGER) or if called, waits until they are needed (LAZY).  

I tend to always use EAGER, more memory intensive, but less error prone. 

 

 

 

Implementing @ManyToMany requires specifying a @JoinTable annotation to determine which table we’re linking to create a Many to Many relationship (This is how we make JOIN TABLES in Spring Data) 

Feel free to investigate, but I typically just use @ManyToOne and @OneToMany together to accomplish the same functionality as @ManyToMany. 

 

 

Other Spring Data Annotations 

 

Spring Data has even more annotations that abstract away the code required for data storage, allowing us to focus more on the business logic. The following is a list and brief explanation of some common Spring Data annotations, which allow us to configure how the queries execute. Usually, defaults are fine, and we won’t need to mess with these. 

These annotations will mostly stay in the DAOs and models 

These are all cAsE sEnSiTiVe!!!  

 

Annotation 

Purpose 

@Transactional 

Indicates that a method should be treated as a transaction. See the Transaction notes below, you’ll often need to use this with updates/deletes. 

@NoRepositoryBean 

Creates an Interface that provides common methods for child repositories. Like making your own version of JpaRepository. Not intended to be used directly for data operations. 

@query & @param 

@query can be used to create your own custom queries with more direct SQL-esque syntax. @param lets you pass parameters to queries defined with @query 

@transient 

Marks a field as transient, to be ignored by the data store. Transient = not persisted to DB.   

 

 

 


■ “EntityManager is the interface that lets us query/manipulate our database from our Java server” -Good QC line

Implementation

- 


JPA is where we get the annotations that map our model classes to DB tables. 

- defined in the `javax.persistence` package
- uses annotations from the JPA to directly map our Java models to Database tables. (So our DB tables get created by our Java models!)
- uses the `EntityManager Interface` to create, read, update and delete (crud) DB entities (tables) and their data in the database. 


`EntityManager Interface`
 - the interface that lets us query/manipulate our database from our Java server (QC line) 

JPA has standardized annotations that we’ll rely on heavily (e.g. @Entity comes from javax.persistence and indicates that a model class is meant to be a DB table).  

 



 


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

