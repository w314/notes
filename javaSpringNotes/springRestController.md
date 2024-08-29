spring, rest, controller

# REST API with Spring Boot

Dependency Needed:
```xml
<dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

- adds `Tomcat` as the embedded servlet container
- by default runs on port `8080`


Change port if needed in `application.properties`:
```bash
server.port = 3456
```
Spring Boot by default reads the static resources such as HTML pages, CSS, Java script, images, etc. present in following locations in classpath:

- /static
- /public
- /resources
- /META-INF/resources

#### Spring Boot Dev Tool
Automates restarting the application when changes are saved.
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <optional>true</optional>
</dependency>
```

## ResponseEntity Class
> A class of the Spring Framework that represents the entire HTTP response, including the status code, headers, and body.
- all handlers have return type `ResponseEntity<T>`
- takes 2 parameters
    - response
    - status code eg: `HttpStatus.OK`

## Annotations

### Define REST Controller

`@RestController`
- defines a REST conroller  
- combination of @Controller
    - creates a bean
- and @ResponseBody
    - values returned by handler methods are written directly to the body of response

### Mapping

`@RequestMapping(value = "/api")`
- maps HTTP resquests to handler methods
- for class level
- could be used at method level like @RequestMapping0(method = RequestMethod.POST) 

`@GetMapping(value = "/customers")`

`@PutMapping(value = "/customers)`

`@PostMapping(value = "/customers/{customerId})`

`@DeleteMapping(value = "/customer/{customerId})`


### Extras values from HTTP requests

`@PathVariable`
- to extract value from URI template variable `\customer\{customerId}`

`@RequestBody`

Extracts value form the body of the request

`@RequestParam`

Binds values form the query string to the controller method parameters.

```java
// http://localhost:8080/infybank/customers?customerId=1234&name=Smith

@GetMapping(value = "/customers")
public ResponseEntity<String> getCustomer(@RequestParam Integer customerId) {
   // ...
```

## Example

```java
// defines a rest controller class
// creates a bean = @Controller
// all responses will be written to response body = @ResponseBody
@RestController
// Defines requests mapped to this controller
@RequestMapping(value = "/api")
public class CustomerAPI {

    // injects service
	@Autowired
	private CustomerService customerService;

    // inject environment variables
	@Autowired
	private Environment environment;

	@GetMapping(value = "/customers")
	public ResponseEntity<List<CustomerDTO>> getAllCustomers() {
		List<CustomerDTO> customerList = customerService.getAllCustomers();

        // returns ResponseEntity
		return new ResponseEntity<>(customerList, HttpStatus.OK);
    }


    // uses @PathVariable
	@GetMapping(value = "/customers/{customerId}")
	public ResponseEntity<CustomerDTO> getCustomer(@PathVariable Integer customerId) {
		CustomerDTO customer = customerService.getCustomer(customerId);
		return new ResponseEntity<>(customer, HttpStatus.OK);
	}

    // uses @RequestBody
	@PostMapping(value = "/customers")
	public ResponseEntity<String> addCustomer(@RequestBody CustomerDTO customer) {
		Integer customerId = customerService.addCustomer(customer);
        //get success message from environment variables
		String successMessage = environment.getProperty("API.INSERT_SUCCESS") + customerId;

        // return CREATED code NOT OK
		return new ResponseEntity<>(successMessage, HttpStatus.CREATED);
	}


	@PutMapping(value = "/customers/{customerId}")
	public ResponseEntity<String> updateCustomer(@PathVariable Integer customerId, @RequestBody CustomerDTO customer) {
		customerService.updateCustomer(customerId, customer.getEmailId());
		String successMessage = environment.getProperty("API.UPDATE_SUCCESS");
		return new ResponseEntity<>(successMessage, HttpStatus.OK);
	}

	@DeleteMapping(value = "/customers/{customerId}")
	public ResponseEntity<String> deleteCustomer(@PathVariable Integer customerId) {
		customerService.deleteCustomer(customerId);
		String successMessage = environment.getProperty("API.DELETE_SUCCESS");
		return new ResponseEntity<>(successMessage, HttpStatus.OK);
	}
}
```

## CORS (Cross Origin Resource Sharing)

- For security reasons browsers do not allow cross origin requests.

- Documents from efg.com cannot request images from yhj.com.

- To allow clients to make calls to the REST API, we can use @CrossOrigin.

- when applied at class level it will be applied ot all methods

```java
@CrossOrigin
@RestController
@RequestBody(value = "/api")
public class CustomerController { }
```