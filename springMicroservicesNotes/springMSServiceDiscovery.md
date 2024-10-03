# Service Discovery with Consul


## Implement Service Discovery 

### 1. Add dependency
- will ensure that the microservice registers itself
- enables the microservice to discover other services

- do exclusion 2:20
    - hystrix
    - netflix ribbon


### 2. Add Configuration

`bootstrap.yml`
```yml
consul:
  discovery:
  #add where discovery server is
    hostname: localhost
```
If you restart the microservices you should be able to see them registered in `Consul` in the `Services` tab.


### 3 Modify Controller Class
Setup controller to get other microservices's uri from the discovery server.

`CustomerController.java`
```java
@RestController
@CrossOrigin
public java class CustomerController {
    
    // autowire dicovery client to fetch urls
    @Autowired
    private DiscoveryClient client;

    // remove lines that get hard coded uri from properties file
    // @Value("${plan.uri}")
    // String planUri;

 
    // modify method to use the autowired client to
    public CustomerDTO get CustomerProfile(@PathVariable Long phoneNo) {

        //...
        // make call to other microservice
        // use microservice name PlanMS
        // returns list of service instances
        List<ServiceInstance> listOfPlanInstances = client.getInstances("PlanMS");
        // check if we have instances
        if(listOfPlanInstances != null && !listOfPlanInstances.isEmpty()) {
            // if we have instances fetch plan URI
            // it will fetch host and port number only
            planUri = listOfPlanInstances.get(0).getUri().toString();
        }
    }
```
Other updetes 
- remove uri from `applicatoin.properties`

 

 

 

