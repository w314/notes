bean-validation-api, spring, validation, input, input-validation

# Bean Validation API
> Used for input validation in Spring.

To use add dependency to `pom.xlm`

```java
<dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-validation</artifactId>
</dependency>
```
## Validate Data Sent in Request Body

### Constraint Validation Annotation

- `@NotNull`	Checks that the annotated property is not null
- `@Null`	Checks that the annotated property is null
- `@Min`	Checks that the annotated property has value greater than or equal to given value
- `@Max`	Checks that the annotated property has value less than or equal to given value 
- `@Email`	Checks that the annotated property is a valid email id
- `@NotEmpty`	Checks that the annotated property is not null or empty for given collection
- `@NotBlank`	Checks that the annotated property is not null or white space
- `@Pattern`	Checks that the annotated property follows the provided regex attribute
- `@Past`	Checks that a date value is in the past
- `@PastOrPresent`	Checks that a date value is in the past including the present date
- `@Future`	Checks that a date value is in the future
- `@FutureOrPresent`	Checks that a date value is in the future including the present date
- `@Size`	Checks that size of annotated property is between its min and max attributes. It can be applied to String, Collection, Map and Array properties.


Cascading Validation
- validating object having reference of other object
- use `@Valid` for referenced objects

### Set Up Validation

#### Set Up Valididation Messages

`src/resources/ValidationMessages.properties`:
```bash
customer.emailid.absent=Please provide email address
customer.emailid.invalid=Please provide valid email address
customer.name.absent=Please provide customer name
customer.name.invalid=Name should contain only alphabets and space
customer.dob.invalid=Date of birth should be past or present date
```

#### Mark DTO with Annotations

```java
public class CustomerDTO {   
    private Integer customerId;
	
    @Email(message = "{customer.emailid.invalid}")
    @NotNull(message = "{customer.emailid.absent}") 
    private String emailId;
	
    @NotNull(message = "{customer.name.absent}")
    @Pattern(regexp="[A-Za-z]+( [A-Za-z]+)*", message="{customer.name.invalid}")
	private String name;
    
    @PastOrPresent(message = "customer.dob.invalid")
	private LocalDate dateOfBirth;
    //getter and setter
}
```
- use `"{ }"` to retrieve messages from ValidationMessages.properties
- adding the constrains on the bean attributes will **NOT** carry out validation
- have to use `@Valid` in the POST request

#### Use @Valid in Controller Methods

```java
@PostMapping(value = "/customers")
public ResponseEntity<String> addCustomer(@Valid @RequestBody CustomerDTO customerDTO) throws InfyBankException  {
   //rest of the code
}
```
- `@Valid` will make Spring validate the incoming customerDTO
- will throw `MethodArgumentNotValidException` if the validation fails


## Validate Path Variables & Request Parameters

```java
@RestController
@RequestMapping(value="/infybank")
@Validated
public class CustomerAPI {
	
	@Autowired
	private CustomerService customerService;
	
	@GetMapping(value = "/customers/{customerId}")
	public ResponseEntity<Customer> getCustomerDetails(@PathVariable @Min(value = 1, message = "Customer id should be between 1 and 100") @Max(value = 100, message = "Customer id should be between 1 and 100") Integer customerId)  throws Exception  {
		Customer customer = customerService.getCustomer(customerId);
		ResponseEntity<Customer> response = new ResponseEntity<Customer>(customer, HttpStatus.OK);
		return response;
	}
```
- use `@Validated` annotaion for the controller class
- use contrainst annotation for setting validation rules
- `ConstraintViolationException` is thrown when validation fails