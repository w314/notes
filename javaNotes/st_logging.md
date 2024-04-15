
## Logging

> What is logging and what are the benefits of it?

> Logging is keeping a log of events that occur form an application.

### Logback

- `Logback` is one of the most widely used logging frameworks in the Java Community.(It's a replacement for its predecessor, Log4j.)
- Logback offers:
  - faster implementation
  - more options for configuration
  - more flexibility in archiving old log files
  - smaller memory footprint

Resons to prefer `Logback` over `Log4j`:

- small and speedy: components are faster and have a smaller memory footprint
- much better tested framework
- automatically reloads configuration files
- gracefully recovers from I/O errors (no need to restart app after server fail, just to get logging to work again)
- automatic removal of old log archives
- automatic compression of archived log files

### Logback Architecture

The `Logback architecture` is comprised of three classes:

- `Logger` - object that allows you to create logs
- `Appender` - represents the destination of a log
- `Layout` - controls log message formatting

### How to use a Logger

> How would we configure logging in an application?

1. configure logger
2. use logger objects in classes you want to use logging
3. use the logger object's logging level method

### Logging Levels

> Describe the different logging levels and how they should be used.

- TRACE - most fine-grained information
- DEBUG - should be used for information that may be needed for diagnosing issues and troubleshooting
- INFO - standard log level
- WARN - indicates that something unexpected happened, but the code can continue the work
- ERROR - hould be used when the application hits an issue preventing one or more functionalities from properly functioning

Setting level at a certain level gives all level on and above that level.

#### Logging Levels Are Used For

What are logging levels good for?

- filtering
- allow you to configure your logging process so that it behaves differently according to each level:
  - Granularity. It might make sense to decrease or increase the granularity of logging according to the level.
  - Target. You might want level X entries to be logged to files, and level Y entries to be logged to a database.
  - Retention policy. This is linked to granularity. If a certain level has a higher granularity, it might make sense to delete the log entries in that level more frequently, for example, to save disk space.

#### Setup & Configuration

- if no configuration is given, default logger can be used
- default logger uses debug logging level
- to configure create `logback.xml` file under `main/resources`
- create appenders
- create loggers and assign them appenders

##### Add dependency to `pom.xml`

`Logback` uses the Simple Logging Facade for Java (`SLF4J`).

`Classpath`
Logback also requires logback-classic.jar on the classpath for runtime.

We'll add this to `pom.xml` as a test dependency:

```xml
<!-- https://mvnrepository.com/artifact/ch.qos.logback/logback-classic -->
<dependency>
    <groupId>ch.qos.logback</groupId>
    <artifactId>logback-classic</artifactId>
    <version>1.4.11</version>
    <scope>test</scope>
</dependency>
```

##### Add `logback.xml` configuration file

We'll create a text file named `logback.xml` and put it somewhere in our classpath:

```xml
<configuration>
  <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
    <encoder>
      <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
    </encoder>
  </appender>

  <root level="debug">
    <appender-ref ref="STDOUT" />
  </root>
</configuration>
```

#### Use Logger

```java
package main;

public class Example {

    // create logger object
    private static final Logger logger = LoggerFactory.getLogger(Example.class);

    // use logging methods
    public static void main(String[] args) {
        logger.info("Example log from {}", Example.class.getSimpleName());
    }
}
```