# Spring Boot Testing

 

To use add dependecy in `pom.xml`:

```java

<dependency>

    <groupId>org.springframework.boot</groupId>

    <artifactId>spring-boot-starter-test</artifactId>

    <scope>test</scope>

</dependency>

```

 

## Testing with JUnit

 

To test the following method:

```java

@Service(value="customerLoginService")

public class CustomerLoginServiceImpl implements CustomerLoginService {

 

    @Autowired

    private CustomerLoginRepository customerLoginRepository;

 

    public String authenticateCustomer(CustomerLoginDTO customerLoginDTO) throws MyException {

        String toRet = null;

        CustomerLoginDTO customerLoginFromRepository =

                customerLoginRepository.getCustomerLoginByLoginName(customerLoginDTO.getLoginName());

        if (customerLoginDTO.getPassword().equals(customerLoginFromRepository.getPassword())) {

            toRet = "SUCCESS";

        } else {

            throw new MyException("Service.WRONG_CREDENTIALS");

        }

        return toRet;

    }

}

```

 

Create a test like:

```java

// @SpringBootTest load the ApplicationContext

@SpringBootTest

public class DemoSpringBootCoreApplicationTests {

 

    // Inject Class of method to test

    @Autowired

    CustomerLoginService customerLoginService;    

 

    // use @Test to mark test methods

    @Test

    public void authenticateCustomerTestValidCredentials() throws MyException {

        CustomerLoginDTO customer = new CustomerLoginDTO();

        customer.setLoginName("monica");

        customer.setPassword("monica123");

        String actual = customerLoginService.authenticateCustomer(customer);

        // Use assertions to test outcome

        Assertions.assertEquals("SUCCESS", actual);

    }

 

    // test for negative outcome also

    @Test

    public void authenticateCustomerTestInValidCredentials() throws MyException {

        CustomerLoginDTO customer = new CustomerLoginDTO();

        customer.setLoginName("monica");

        customer.setPassword("monica13");

        MyException exception=Assertions.assertThrows(MyException.class,()->customerLoginService.authenticateCustomer(customer));

        Assertions.assertEquals("Service.WRONG_CREDENTIALS", exception.getMessage());

    }

}

```

- `@SpringBootTest` loads ApplicationContext using SpringApplication so that all the Spring Boot features will be available to the tests

 

## Testing with Mockito

 

In the example above CustomerLoginService depends on CustomerLoginRepository.

 

To test CustomerLoginService independently a `mocking framework` can help mock the behaviour of the dependency. You use a mock object instead of the actual that returns that data required for the testing.

 

### Create Mock Objects

 

The `@Mock` annotation marks the field to be mocked.

```java
@Mock
CustomerLoginRepository customerLoginRepository;
```

 

To create a mock object use `@InjectMocks`

```java
@InjectMocks
CustomerLoginService customerLoginService =  new CustomerLoginServiceImpl();
```

 

### Add Behavior to Mock Objects

 

Methods used to add behavior are described in the `org.mockito.Mockito` class.

 

#### `when`

- static method

- specifies value returned

 

```java

Mockito.when(customerRepository.getCustomerByCustomerId(1002)).thenReturn(null);

```

 

Use `matcher methods` for a range of values:

```java

Mockito.when(customerRepository.getCustomerByCustomerId(anyInt())).thenReturn(null);

```

 

- `anyBoolean()` returns any boolean or Boolean value

- `anyInt()` returns any integer or Integer value

- `anyFloat()` returns any float or Float value

- `anyDouble()` returns any double or Double value

- `anyLong()` returns any long or Long value

- `any()` returns any Object

 

Take care!:

- `private` and `static` method CANNOT be mocked

- never use matchers for return values

- methods for multiple arguments provide mathers or exact values for all

- matcher methods can only be used for verification or stubbing