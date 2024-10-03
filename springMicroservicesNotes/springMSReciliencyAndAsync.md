# Resiliency

## Cercuit Braker Pattern

### States of Curcuit Breaker
- Closed
    - after a set failure rate the circuit will open
- Open
    - after set wait time enters in to half-open state
- Half_Open
    - checks state of services
    - goes on to open or closed state based on that 

### Types of Circuit Breaker Pattern

#### Count-based sliding window
Change of state is dependent on the number requests received/failed

Configuration:

#### Time-based sliding window
Configurations needed:
- slidingWindowTYpe: TIME_BASED

time in millisecond after which a call is considered slow
- slowCallDurationThreshold: 4000

percentage of call that have to fail during that time:  
- slowCallRateThreshold: 50


### Exceptions
By default all exceptions count as a failure.

We can define a list of exception that count as a failure, in that case all other exceptions are considered a success.
 
Exception can also be ignored.

## Implement Resiliency with `Resilience4j`

### 1. Add dependency

`pom.xml`
```xml
<dependency>
    <groupId>resilience4j-spring-boot2</groupId>
    <a>
</dependency>

<dependency>
    <groupId></groupId>
    <artifactId>spring-boot-starter-aop</artifactiId>
</dependency>

```

### 2. Configure `Resilience4j`

Add new `application.yml` file:
```yml
resilience4j.circuitbreaker:
  instances:
    customerService:
    # if 50% or more of the calls fail it will open the circuit
      failureRateThreshold: 50
    #    a
      ringBufferSizeInClosedState: 50
      ringBufferSizeInHalfOpenState: 3
    #   time application should wait before closing the circuit again
      waitDurationInOpenState: 20s
    #   set it to auomatically move from open to half open state
      automaticTransitionFromOpenToHalfOpen: true
```

### 3. Update Controller Class

`CustomerController.java`
```java
@RestController
@CrossOrigin
public class CustomerController {

    // update method
    // add annotation @CircuitBreaker
    // for name use instances name from application.yml file
    // add fallbackMethod
    @CircuitBreaker(name="customerService", fallbackMethod="getCurtomerProfilefallback")
    @GetMapping(value="/customers/{phoneNo}", produces=MediaType.APPLICATION_JSON_VALUE)
    public getCutomerProfile(@PathVariable Long phoneNo) {

        // method code
    }

    // create fallback method
    // use same method signature of actual method
    // optional exception parameter may be added
    public CustomerDTO getCustomerProfileFallback(Long phoneNo, Throwable throwable) {
        // return empty customerDTO
        return new CustomerDTO();
    }
}
```

### 4. Add new Circuit Breaker Service

`services/CustCircuitBreakerService.java`

 ```java
@Service 
public class CustCirtuitBreakerService {

    // autowire load balanced rest template
    @Autowired
    RestTemplate template;

    // add circuit breaker annotation
    // for name use instances name from application.yml file
    // the purpose is not to show resiliency here so no fallback method needed
    @CircuitBreaker(name="customerService")
    public PlanDTO getSpecificPlan(Integer planId) {
        return template.getForObject("http://PlanMS/plans/"+planId, PlanDTO.class);
    }

    @CircuitBreaker(name="customerService")
    @SuppressWoarning("unchecked") // do not know what is this
    public List<Long> getSpecificFriends(Long phoneNo) {
        return template.getForObject("http://FriendMS/customers/"+phoneNo+"/friends", List.class);
    }
}
```

### 5. Use CircuitBreakerService in Controller Class

`CustomerController.java`
```java
public class CustomerController {

    // remove autowired loadbalanced rest template
    // autowire circuit breaker service
    @Autowired
    CustCircuitBreakerService custCircuitBreakerService;

    // update method
    @CircuitBreaker(name="customerService", fallbackMethod="getCurtomerProfilefallback")
    @GetMapping(value="/customers/{phoneNo}", produces=MediaType.APPLICATION_JSON_VALUE)
    public CustomerDTO getCustomerProfile(@PathVariable Long phoneNo) {
        //...
    
        // change calls to other microservices
        // to get plan details
        PlanDTO planDTO = custCircuitBreakerService.getSpecificPlan(custDTO.getCurrentPlan().getPlanId(););

        // set plan with received details
        custDTO.setCurrentPlan(planDTO);

        // to get friend list
        List<Long> friends = custCircuitBreakerService.getSpecificFriends(phoneNo);

        // set friend list
        custDTO.setFriends(friends);
    }

}
 

 # Async Communication in Spring Microservices

- Sending paralell requests to other microservices
- reduces turnaround time

## Implement Async Communication with `Future` object

FUture is a computational object that will be available in the future.

### 1. Return Future when calling a microservice
`services/CustCircuitBreakerService.java`
```java
@Service
public class CustCircuitBreakerService {

    
    // autowire load balanced rest template
    @Autowired
    RestTemplate template;

    @CircuitBreaker(name="customerService")
    // return Future<PlanDTO> instead of PlanDTO in function signature 
    public Future<PlanDTO> getSpecificPlan(Integer planId) {
        // return Future<> from function
        // Future.of takes a lambda expression
        return Future.of(() -> template.getForObject("http://PlanMS/plans/"+planId, PlanDTO.class));
    }

    @CircuitBreaker(name="customerService")
    @SuppressWoarning("unchecked") // do not know what is this
    public Future<List<Long>> getSpecificFriends(Long phoneNo) {
        return Future.of(() -> template.getForObject("http://FriendMS/customers/"+phoneNo+"/friends", List.class));
    }
}
```

### 2. Modify Contoller Class to accept Future<>

`CustomerController.java`
```java


        // change calls to other microservices
        // to receive Future
        Future<PlanDTO> planDTOFuture = custCircuitBreakerService.getSpecificPlan(custDTO.getCurrentPlan().getPlanId());

        // to get friend list
        Future<List<Long>> friendsFuture = custCircuitBreakerService.getSpecificFriends(phoneNo);

        // move setting customer profile properties to the end of the method not right after the calls
        // get value from future with .get()

        // set plan with received details
        custDTO.setCurrentPlan(planDTOFuture.get());
        // set friend list
        custDTO.setFriends(friendsFuture.get());
```    