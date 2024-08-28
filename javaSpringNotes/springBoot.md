springboot, java, spring

# Spring Boot

Downside of plain Spring Applications
- Configuration
    - requires a lot of configuration
    - configuration needs to be overwritten for different environment
    - => lot of time spent on writing configuration instead of the application
- Dependency Management
    - have to search for dependencies
    - have to manually configure them

Productivity suffers.

Here comes Spring Boot

## Spring Boot

- built on top of the Spring Framework
- it's main goal to let developers create Spring based application quickly withour writing the same boilerplate configuration again and again
- **opinionated** framework
- uses embedded **Tomcat server** as the default web container
- **customizable**

### Main Feauters
- starter dependencies
- automatic configuration
- spring boot actuator
- embedded servlet container


## Spring Boot Application

Annotated with `@SpringBootApplication` annotation:
- indicates it is a configuration class
- triggers auto-configuration
- triggers component-scanning

It is a combination of the following annotations:
- `@EnableAutoConfiguration`
- `@ComponentScan`
- `@Configuration`


A Spring Boot Application is configured by the `application.properties` file found under `src/main/resources`.

To use a custom property:
- add to `application.properties` file
- it will be automatically added to the Spring  `Environment Class` at startup
- the Environment Class should be autowired into any class that needs it
- read the property using the `getProperty()` method of the Environment Class

