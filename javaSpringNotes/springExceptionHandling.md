java, spring, spring-boot, exception, exception-handling

# Exception Handling in Srping

## Using @RestControllerAdvice

### Create ErrorInfo Class 

To provide more informaion about erros, it is best to create an error infor class.

```java
public class ErrorInfo  {
            private String errorMessage;
            private Integer errorCode;
            private LocalDateTime timestamp;
    //getters and setters
}
```

### Set up Exception Controller Advice

```java
// mark it as @RestControllerAdvice
@RestControllerAdvice
public class ExceptionControllerAdvice {

    // Inject environment variables
    @Autowired
    Environment environment;
            
    // mark exception handler methods with @ExceptionHandler
    // give the type of exception handles as ExceptionTYpe.class
    // if there is more handled use { Exception1.class, Exception2.class }
    @ExceptionHandler(Exception.class)
    // returns ResponsEntity of ErrorInfo Type
    // takes the handled exception as an argument          
    public ResponseEntity<ErrorInfo> exceptionHandler(Exception exception) {
        
        // create new errorInfo object
        ErrorInfo error = new ErrorInfo();
 
        // set error details
        error.setErrorMessage(environment.getProperty("General.EXCEPTION_MESSAGE"));                
        error.setErrorCode(HttpStatus.INTERNAL_SERVER_ERROR.value());       
        error.setTimestamp(LocalDateTime.now());
 
        // return HTTP response
        return new ResponseEntity<ErrorInfo>(error, HttpStatus.INTERNAL_SERVER_ERROR);    
 }
```
If no exceptionType is set with the annotation the exceptions that the method takes as an argument will be handled by default.

## Using ResponseStatusException Class
> Base class for exceptions associated with HTTP status codes.


```java
@GetMapping(value = "/customers/{customerId}")
public ResponseEntity<CustomerDTO> getCustomer(@PathVariable Integer customerId) {
		try {
			CustomerDTO customerDTO = customerService.getCustomer(customerId);
			return new ResponseEntity<>(customerDTO, HttpStatus.OK);
		} catch (Exception exception) {
			throw new ResponseStatusException(HttpStatus.NOT_FOUND, environment.getProperty(exception.getMessage()), exception);
		}
}
```
To create an instance provide:
- HTTP status code
- message to explain the exception
- exception
