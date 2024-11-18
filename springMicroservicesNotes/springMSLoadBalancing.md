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
Supoorts both static and dynamic load balancing.

Sources:
- Source: [Sping Docs](https://spring.io/guides/gs/spring-cloud-loadbalancer) - static example

- Source: [maybe dynamic example?](https://spring.io/guides/gs/service-registration-and-discovery)

### 1. Update Configuration in Consul

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
  # need unique instance id for consul 
  # to register more than 1 service
  cloud:
    consul:
      discovery:
        instanceId: ${spring.application.name}:${vcap.application.instance_id:${spring.application.instance_id:${random.value}}}
```

### 2. Run Several MS instances

To start several instance of a microservice in Sprint Suite:
- right click microservice
- duplicate configuration
- run all services


### 3. Use Spring Cloud Load Balancer in Microservice

Use Spring Cloud Load Balancer to load balance requests to the microservice with several instances running.

#### 3.1 Add Dependency

`pom.xml`
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-loadbalancer</artifactId>
</dependency>
```
### 3.2 Create Load Balanced RestTemplate
For the controller to use when contacting other microservices.

`src/main/java/CustomerConfig.java`
```java
// use the @Configuarton annotation
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
### 3.3  Use Load Balancing in Controller Class

Setting up ownerMS to use load balancing when using petMS:

Update `src/main/java/controller/ownerController.java`
```java
public class CustomerController {

    // autowire load balanced RestTemplate
    @Autowire
    RestTemplate template;

    // remove variable to store petUri
    // private String petUri ;


    // remove getting uli-s from service registry
    /*
        // get petMS microservice urls from service registry
       List<ServiceInstance> listOfPetInstances = client.getInstances("petMS");
       if(listOfPetInstances != null && !listOfPetInstances.isEmpty()) {
       	petUri = listOfPetInstances.get(0).getUri().toString();
      }
    */

    // WHEN CONTACTING THE PET MICROSERCIE
    // remove
    // define pet microservice url for getting pet details
    // String petUrl = petUri + "/pets/" + petId;
    // instead of using
    // PetDTO petDTO = new RestTemplate().getForObject(petUrl,PetDTO.class);
    
    // use load balanced template when making API calls to other microservices
    // add MS name and form url as needed
    PetDTO petDTO = template.getForObject("http://petMS/pets/"+petId,PetDTO.class);
```




## Implement Static Load Balancing 

- uses same `spring-cloud-starter-loadbalancer` dependency
- uses fixed port numbers in configuration
- this example does not use service discovery

### Configuration for `Static` Load balancing

- Use the same OwnerConfig class for to create a load balanced `RestTemplate` as for dynamic load balancing.
- For static load balancing provide the instances to balance in a configuration class:

Create a Load Balancer configuration class.

`src/main/java/com.wp.ownerMS/LoadBalancerConfig.java`
```java
@Component
public class LoadBalancerConfig {
	@Bean
	@Primary
	ServiceInstanceListSupplier serviceInstanceListSupplier() {
		return new OwnerServiceInstanceListSupplier("petMS");
	}	
}

class OwnerServiceInstanceListSupplier implements ServiceInstanceListSupplier {
	
	private final String serviceId;
	
	OwnerServiceInstanceListSupplier(String serviceId) {
		this.serviceId = serviceId;
	}
	
	@Override
	public Flux<List<ServiceInstance>> get() {		
		return Flux.just(Arrays.asList(
			new DefaultServiceInstance(serviceId + "1", serviceId, "localhost", 7300, false), 
			new DefaultServiceInstance(serviceId + "2", serviceId, "localhost", 7400, false)
		));
	}
	
	@Override
	public String getServiceId() {
		return this.serviceId;		
	}
}
```
- whenever a service name MyloadBalancer is contacted it will use the configuration form teh LoadBalancerConfig.class
- The LoadBalancerConfig.class configuraton calss will provide the list of static URLs among which the request has to be balanced


### Update Controller Class

`src/main/java/controller/OwnerMS.java`
```java
// add annotation for Load Balancing
// specify configuration file and add a name to the load balancer
@LoadBalancerClient(name="MyLoadBalancer", configuration=LoadBalancerConfig.class)
public class OwnerController {

    // autowire load balanced RestTemplate
    @Autwired
    RestTemplate template;

    // ...

    // contact pet micoservice for pet details
    // using load balanced template
    int petId = 2;
    // use the autowired load balanced rest template 
    // to contact pet MS
    // in the url use the loadBalacer name provided in the
    // @LoadBalancerClient annotation
    PetDTO petDTO = template.getForObject("http://MyLoadBalancer/pets/"+petId, PetDTO.class);
}


