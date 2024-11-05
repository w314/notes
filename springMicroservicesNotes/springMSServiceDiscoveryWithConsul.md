# Service Discovery
The following API service registry and discovery of micreservices:
- Cloud Consul
- Eureka

Sources
- [Spring Documentation](https://docs.spring.io/spring-cloud-consul/reference/discovery.html)

## Implement Service Discovery With Consul 

### 1. Add dependency
`pom.xml`
```xml
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-consul-discovery</artifactId>
        </dependency>
```
- will ensure that the microservice registers itself
- enables the microservice to discover other services

### 2. Add Configuration

Consul server is by default running on `localhost:8500`.

If it is not the case for the consul server of the project it can be configured in the `application.yml` file:
```yml
spring:
  cloud:
    consul:
      host: localhost
      port: 8500
```
If you restart the microservices you should be able to see them registered in `Consul` in the `Services` tab.


### 3 Modify Controller Class
> To make our controller get other microservices's uri from the discovery server we need the `DisocveryClient Class`. 

Use:

`import org.springframework.cloud.client.discovery.DiscoveryClient;`

The Controller below calls the registryMS microservice to retrieve a list of pet id's that belong to the owner.
```java
// import DiscoveryClient
import org.springframework.cloud.client.discovery.DiscoveryClient;
// other imports

@RestController
@RequestMapping
public class OwnerController {

    @Autowired
    OwnerService ownerService;
    
    // autowire DiscoveryClient
    @Autowired
    private DiscoveryClient client;

    // define variables to store microservice urls
    private String registryUri;
    private String petUri ;

    @GetMapping("/owners")
    public ResponseEntity<List<gOwnerDTO>> getOwners() {
        List<OwnerDTO> ownerDTOS = this.ownerService.getOwners();
        return new ResponseEntity<>(ownerDTOS, HttpStatus.OK);
    }

    @GetMapping("/owners/{ownerId}")
    public ResponseEntity<OwnerDTO> getOwner(@PathVariable int ownerId) {
    	
    	// get owner from service
    	// this will include an empty list of petDTOs
        OwnerDTO ownerDTO = this.ownerService.getOwnerById(ownerId);
        System.out.println(ownerDTO);
        
        // use service discovery to get microservice urls
        // get registryMS microservice urls from service discovery
        // use microservice name
        // returns list of serviceIntance (can be several instances of the MS running)
        List<ServiceInstance> listOfRegistryInstances = client.getInstances("registryMS");
        // check if there is at least one instance returned
        if(listOfRegistryInstances != null && !listOfRegistryInstances.isEmpty()) {
        	// get microservice uri from the first instance
        	// will contain host and port number
        	registryUri = listOfRegistryInstances.get(0).getUri().toString();
        	System.out.println("REGISTRY URL: " + registryUri);
        }
        
        
        // define registry microservice url needed to get list of pet ids
        String registryUrl = registryUri + "/owners/" + ownerDTO.getId() + "/pets";
        // get the ids of pets belonging to the owner
        List<Integer> petIds = new RestTemplate().getForEntity(registryUrl, List.class).getBody();
        
        // rest of the code
    }
}
```
Other updetes 
- remove uri from `application.properties`

 

 

 

