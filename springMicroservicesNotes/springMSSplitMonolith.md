# Separate Monolith to Microservices

## Database Separation
- set up separate db for each microservice
- remove remove foreign keys from the table
- correct `spring.datasource.url` in the `application.properties` file

## Connecting the Microservices
THIS IS A TEMPORARY SOLUTION, AFTER THE MICROSERVICES ARE SET UP THERE WILL BE NO NEED FOR USING RestTemplate.

Use `RestTemplate` to make API calls to other microservices.


In the following example the ownerController class would like to display an owner with the information of all its pets.
- to do that is has to connect to the registryMS microservice to find out the pets the owner has
- and has to connect the petMS microservice to find out the details of those pets
```java
@RestController
@RequestMapping
public class OwnerController {

    @Autowired
    OwnerService ownerService;

    // get uri-s of other microservices needed
    // form the 'application.properties' file
    @Value("${registryUri}")
    String registryUri;
    @Value("${petUri}")
    String petUri;

    // display owner and its pets
    @GetMapping("/owners/{ownerId}")
    public ResponseEntity<OwnerDTO> getOwner(@PathVariable int ownerId) {
    	// get owner from service
    	// this will include an empty list of petDTOs
        OwnerDTO ownerDTO = this.ownerService.getOwnerById(ownerId);
        // define registry microservice url needed to get list of pet ids
        String registryUrl = registryUri + "/owners/" + ownerDTO.getId() + "/pets";
        System.out.println(registryUrl);
        // get the ids of pets belonging to the owner
        List<Integer> petIds = new RestTemplate().getForEntity(registryUrl, List.class).getBody();
        // create empty petDTO array to store pet information
        List<PetDTO> petDTOS = new ArrayList<>();
        // get details for each pet that belongs to the owner
        for(Integer petId: petIds) {
        	// define pet microservice url for getting pet details
        	String petUrl = petUri + "/pets/" + petId;
        	System.out.println(petUrl);
            PetDTO petDTO = new RestTemplate().getForObject(petUrl,PetDTO.class);
            petDTOS.add(petDTO);
        }
        // use the information received from the pet microservice 
        // to set the pets property of the owner
        ownerDTO.setPets(petDTOS);
        return new ResponseEntity<>(ownerDTO, HttpStatus.OK);
    }
}
```