# Load Balancing
> Load balancing is the process of distributing traffic among different instances of the same application.

## Sources
- [Baeldung Spring Cloud Load Balancer](https://www.baeldung.com/spring-cloud-load-balancer)
- [Geeks for Geeks Load Balancing in Spring Boot Microservices](https://www.geeksforgeeks.org/load-balancing-in-spring-boot-microservices/)

## Load Balancing Strategies

There are many algorithms used for o load balancing:
- random selection
    - choosing an instance randomly
- round-robin
    - choosing an instance in the same order each time
- least connections
    - choosing the instance with the fewest current connections
- weighted metric
    - using a weighted metric to choose the best instance
    - for example, CPU or memory usage
- IP hash
    - using the hash of the client IP to map to an instance

## Types of Load Balancing
- Server-Side
- Client-Side

### Server-Side Load Balancing
> A hardware load balancer is put in front of the microservice instances.
- requests are first sent to the load balancer
- it it the load balancer responsibility to decide which microservice to send the request to

Possible problem:
- if the load balancer fails it all fails
- we need a separate load balancer for all microservices
- increases network latency 
    - request has to first to load balancer
    - than to microservice

### Client-Side Load Balancing
> Client-side load balancer is a softwer, where the client decides which microservice instance should recieve the request.

Types:
- static load balancing: 
    - you provide info about where the microservices are running and how many instances are running
    - will not check if ms is down, will keep sending requests
- dynamic:load balancer 
    - interacts with server registry and chooses only the instances that are up and running dynamically

## Client-Side Load Balancing with Spring Cloud Load Balancer

Source: [Sping Docs](https://spring.io/guides/gs/spring-cloud-loadbalancer) - static example

Source: [maybe dynamic example?](https://spring.io/guides/gs/service-registration-and-discovery)

### 1. Run Several MS instances

Run several instances of one of the microservices.

Source: [Spring: Making instance id unique](https://docs.spring.io/spring-cloud-consul/reference/discovery.html#making-the-consul-instance-id-unique)

To allow several instances to run change microservice configuration:

`config/application/data`
```yml
# server config
server:
  # setting port to 0 
  # will make consul choose 
  # random port number
  port: 0
spring:
  # db config
  datasource:
    username: root
    password: password
  jpa:
    hibernate:
      ddl-auto: update
  # unique instance id configuration
  cloud:
    consul:
      discovery:
        instanceId: ${spring.application.name}:${vcap.application.instance_id:${spring.application.instance_id:${random.value}}}
```

To start several instance of a microservice in Sprint Suite:
- right click microservice
- duplicate configuration
- run all services


### Use Spring Cloud Load Balancer in Microservice

Use Spring Cloud Load Balancer to load balance requests to the microservice with several instances running.

#### Add Dependency

`pom.xml`
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-loadbalancer</artifactId>
</dependency>
```

#### Configure Load Balancer

`src/main/java/com.wp.ownerMS/LoadBalancerConfig.java`
```java


#### Use Load Balancer in Controller Class

```java
@LoadBalancerClient(name="MyloadBalancer", 
configuration=LoadBalancerConfig.class)
```
- whenever a service name MyloadBalancer is contacted instead of using the default setup it will use the configuration form teh LoadBalancerConfig.class
- The LoadBalancerConfig.class configuraton calss will provide the list of static URLs among which the request has to be balanced


## Implement Dynamic Load Balancing

### 1. Create Load Balanced RestTemplate

Create `src/main/java/CustomerConfig.java`
```java
@Configuration
public class CustomerConfig {

    // create load balanced RestTemplate 
    // to be used whenever it is needed
    // when other microservices are called
    @Bean 
    @LoadBalanced
    RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```

### 2. Use Load Balanced RestTemple in Controller

`CustomerController.java`
```java
public class CustomerController {

    // autowire load balanced RestTemplate
    @Autowire
    RestTemplate template;

    // use load balanced template when making API calls to other microservices
    public CustomerDTO getCutomerProfile(@PathVariable Long phoneNo) {

        // earlier got a list of ServiceInstance and used the first
    }
}
```

### Dynamic Load Balancing with `Consul`


### Static Load Balancing with `Spring Cloud Load Balancer`
 
### 1. Add dependency

`pom.xml`
```xml
spring-cloud-load-balancer
```

### 2 Configure Load balancer

Demo-Load balance: 1:35

Create `src/main/java/LoadBalancerConfig.java`
```java
@Component
public class LoadBalancerConfig {}
```


