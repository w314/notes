# Load Balancing

Types:
- server-side
- client-side

 

### Server-side 
Possible problem:
- if the load balancer fails it all fails
- we need load balancer for all microservices

### client-side load balancer

- softwer, client side decides where to send the requets

Types:
- static load balancing: you provide info about where the microservices are running and how many instances are running
- dynamic:load balancer interacts with server registry and chooses only the instances that are up and running dynamically

## Implement Load Balancing

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


