# Spring Caching

> In `Cashing` frequently accessed data is stored in cache memory so that data can be accessed faster for future requests.

 

- Boosts the performance of applications.

- Spring provides method level caching. (If a method is called with the same parameters no need to execute the method again.)

 

## How to use Cashing in Spring

 

### Add dependency

 

`pom.xml`

```java

<dependency>

     <groupId>org.springframework.boot</groupId>

     <artifactId>spring-boot-starter-cache</artifactId>

</dependency>

```

- automatically configures caching using **Simple** provider

- uses **concurrent map** for chaching data

 

### Configure CasheManager if needed

You can configure a bean type CasheManager. It is optional.

 

### Enable Cashing

 

To enable cashing use `@EnableCaching` to annotate the main class.

 

```java

@SpringBootApplication

@EnableCaching

public class DemoSpringBootCoreApplication implements CommandLineRunner {

}

```

 

### Annotate Methods

 

Use `@Casheable` to annotate method to be cashed

```java

@Repository(value = "customerRepository")

public class CustomerRepositoryImpl implements CustomerRepository {

    @Cacheable("customer")

    public Customer getCustomerDetails(Integer customerId) throws MyException {

             // ...

    }

}

```

- the parameter "customer" is the name of the cache the results will be stored

 

## Cashe Annotation used in Spring Boot

 

Below are the caching annotations supported by Spring Boot:

 

- `@Cacheable`: Triggers cache population

- `@CachePut`: Used to update the cache, without interfering the method execution

- `@CacheEvict`: Triggers cache eviction[from cache items could be removed]

- `@Caching`: Regroups multiple cache operations to be applied on a method

- `@CacheConfig`: Shares few common cache-related settings at class-level

`@EnableCaching`: Configuration level annotation, enables caching

 