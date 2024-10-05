# Declarative Client


## Need for Declarative Client
- At this point we use `RestTemplate` to make calls to other microservices.

- Using `RestTemplate` with `Load Balancing` and `CircuitBreaker` is cumbersome.

### Disadvantates of `RestTemplate`
- need to know RestTemplate methods
- need separate Bean for Load Balancing
- need separate service for Circuit Breaker


## Declarative Client
- integrates with Load Balancing APIs
- integrates with Circuit Breaker APIs
- and provides both

## Feign

Declarative client from Netflix.

### How Feign works
- microservice defines interface
- Feign creates implementation

### Advantages
- load balancing
    - Feign uses a load balancer
    - so calls are automatically load balanced
    - uses `ribbon` for load balancing
- resiliency
    - with proper dependencies 
    - it will provide resiliency 
    - without a circuit breaker class

## Implementing Declarative Client with Feign

We will replace RestTemplate with FeignClient.

### 1. Add dependency

`spring-cloud-starter-openfeign`

### 2. Add @EnableFeignClients to app

```java
@SpringBootApplication
@EnableFeignClients
public class CustomerApplication {
    public static void main(String[] args) {
        SpringApplication.run(CustomerApplication.class, args);
    }
}
```

### 3. Add Interfaces for Feign Clients
Have to create an interface for each microservie our microservice are making API class to.


`src/main/java/controller/CustPlanFeign`
```java
// add FeignClient annotation
@FeignClient(name="PlanMS",url="http://localhost:9000" )
public interface CustPlanFeign {

    // create method for API call
    // add @RequestMapping annotation
    @RequestMapping(value="/plans/{planId}")
    PlanDTO getSpecificPlan(@PathVariable(planId) int planId);
     
}
```
- annotate with @FeignClient
- `name` will be name of the microservice we are making calls to
- `url` will be the url of the `gateway` as that is where we get the url of the other microservice


### 3. Use Feign Clients to make calls in Circuit Breaker Service Class

`service/CircuitBreakerService.java`
```java
@Service
public class CircuitBreakerService {

    // autowire each feign client
    @Autowired
    CustPlanFeign planFeign;

    // add method to call microservice using feign client
    // name if @CircuitBreaker annotation
    // refers to the instance name 
    // in the resilience4j.circuitbreaker: configuration
    // in the application.yml file 
    @CircuitBreaker(name="customerService")
    public Future<PlanDTO> getSpecificPlan(Integer planId) {
        return Future.of(() -> planFeign.getSpecificPlan(planId));
    }
}
```
With this we have replacd using RestTemplate with FeignClient.