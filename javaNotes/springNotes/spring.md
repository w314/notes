spring, java, ioc, inversion-of-control, dependency-injection

# Spring Framework

## Why use Spring in project?
Dependency Injection.
- provides loose coupling, more flexible
- easier to test

> `Dependency Injetion` is a technique where an external framwork is responsible for creating, assempling and wiring the dependencies.

> `Inversion of Control` means the control over creating, wiring and assembling an object no longer resides with the dependent classes themselves but with a `Dependency Injection Framework` also called `IoC Containers`


Spring framework is one of the Dependency Injection Framworks avaialble.


## Advantages of the Spring Framework


## Spring IoC Container
> The `IoC Container` creates, initialized and injects the required objects. The life cycle of these objects are managed by Spring. They are called `Beans`.


Spring needs information about these objects, their classes, how to wire them together. 

`Configuration metadata` provides this information. It can provide it in the following ways:
- XML configuration
- Java-based configuration
- Java Annotation based configuration


Spring IoC Container reads application classes, and the configuration metadata to create and wire beans.
![alt text](images/sprintIoC.png)


### Spring IoC Container Interfaces

#### `BeanFactory Interface`

- using its `getBean()` method you can get instances of beans
- beans are only initiated only when asked be the client by calling `getBean()`

#### `Application Context Interface`
- it initiates all beans when the container is loaded
- commonly used implementation of the interface
    - `ClassPathXmlApplicationContext` processes XML based configuration data
    - `AnnotationConfigApplicationContext` processes Java based configuration metadata


## Java based Configuration Metadata

Java based configuration metadata is provided in a Java class using the following annotation:
- `@Configuraion` identifies the class as a configuration class
- `@Bean` declares a bean
    - by default only one instance is created (singleton)
    - by default the name of the bean is the name of the method it is configured
    - that can be changed by adding `@Bean(name="newName")`

```java
@Configuration
public class SpringConfig {

    @Bean
    public CustomerLoginService customerLoginService() {
        return  new CustomerLoginServiceImpl(customerLoginRepository());
    }

    @Bean(name="customerRepository")
    public CustomerLoginRepository customerLoginRepository() {
        return new CustomerLoginRepositoryImpl();
    }

}
``` 

## Java Annotation Based Configuration
No need the for a configuration class, Spring automatically 
detects and intitiates the beans through component scanning.

However scanning is NOT enabled by default, you have to use the `@ComponentScan` annotation to enable component scanning.
```java
@Configuration
@ComponentScan
public class SpringConfig {
}
```

It looks for classes annotated with:
- `@Component` marks a Spring bean (general purpose)
- `@Service` defines a service layer spring bean
- `@Repository` defines a persistent layer spring bean
- `@Controller`defines a web component for the presentation layer


The name of the bean by default is the name of the class just lowercase. To change that use the `value` attribute.
```java
​@Repository(value="customerLogin")
public class CustomerLoginRepositoryImpl implements CustomerLoginRepository {	
	// ...
}
```

Best Practices
- Use specialised annotation over generic
- Annotate classes not interfaces (class implementing an interface does not inherit the annotations)


### Using annotation based configuration

```java
// load context
ApplicationContext ctx = new AnnotationConfigApplicationContext(SpringConfig.class);


// accessing beans
// by class
UserService userService = ctx.getBean(CustomerLoginServiceImpl.class);
// OR
// by the name of the method it is configured
UserService userService = (UserService) ctx.getBean("customerLoginServiceImpl");

```

 <hr>
 <hr>
 <hr>
 OLD NOTES

developer can focus on logic not configuration
dependency injection

- it is a lightweigth application framework


Spring replaced EJB (Enterprises Java Bean)

without sublet container you could nto use spring container

Why are you using tomcat

tomcat is a webserver = server that will manage web container


spring container is inside servlet container
tomcat container 

security you will implemetn at teh container level not the bean level

what is lightweight


third party services you inject into container, all the beans inside can use that service


spring container does not have inbuilt services inside therefore it is lightweigt.

If you need services you can inject them.

____________________________

If i change the nam eof the controller 

how does @ComponentScan

if I change com.wp.contorller to com.controller will Spring recongize the controller class?

@ComponentScan is already included with @SpringBootApplication annotation.
it will scan groupid.artifactid (com.wp.controller)

what if you want to scan some user defined pacakges
if you want different packages you have to overwrite the default ComponentScan with
@ComponentScan(basePackages = {"com.*})

Difference between web application and web services?
web service not dependent on language
web app is langugage dpeendent


web services uses mediator that create an API from service


aservices are API-s , response goes to client =in JSON format. JSON response is created by jackson JSON
Jackson library converts response to JSON

default response of controller is 
