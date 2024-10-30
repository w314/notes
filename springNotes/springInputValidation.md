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

Constaint validation annotation check that the annotated propert is: 
- `@NotNull` 
    - not null
- `@Null`
    - null
- `@Min`
    - has value greater than or equal to given value
- `@Max`
    - has value less than or equal to given value 
- `@Email`
    - a valid email id
- `@NotEmpty`
    - not null or empty for given collection
- `@NotBlank`
    - not null or white space
- `@Pattern`
    - follows the provided regex attribute
- `@Past`
    - in the past
- `@PastOrPresent`
    - in the past including the present date
- `@Future`
    - in the future
- `@FutureOrPresent`
    - in the future including the present date
- `@Size`
    -  between its min and max attributes
    - can be applied to properties that are:
        - String
        - Collection
        - Map
        - Array


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
    
    @PastOrPresent(message = "{customer.dob.invalid}")
	private LocalDate dateOfBirth;
    //getter and setter
}
```


- use `"{ }"` to retrieve messages from ValidationMessages.properties
- adding the constrains on the bean attributes will **NOT** carry out validation
- have to use `@Valid` in the POST request

### Set up Validation in Controller Class


#### use `@Validated` for the controller class
```java
@RestController
@RequestMapping(value="/api")
@Validated
public class CustomerController {...}
```
- using `@Validated` for the controller class triggers validation

#### use `@Valid` to validate request body input
```java

    @PostMapping(value = "/customers")
    public ResponseEntity<String> addCustomer(@Valid @RequestBody CustomerDTO customerDTO) throws InfyBankException  {...}
```
- `@Valid` will make Spring validate the incoming customerDTO
- will throw `MethodArgumentNotValidException` if the validation fails


### validate path variables

```java	
	@GetMapping(value = "/customers/{customerId}")
	public ResponseEntity<Customer> getCustomerDetails(
        @PathVariable 
        @Min(value = 1, message = "Customer id should be between 1 and 100") 
        @Max(value = 100, message = "Customer id should be between 1 and 100") 
        Integer customerId)  throws Exception  {...	}
```
- use contrainst annotation for setting validation rules for path variables
- `ConstraintViolationException` is thrown when validation fails