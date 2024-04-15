
## Testing

### TDD

> What is test driven development?

The `TDD` process consists of writing unit tests first, **before** the implemented application code has been written.

Then, the implemented application code can be written to make the test pass and the process can be completed for each piece of functionality required.

When refactoring code, the unit tests give us confidence that we can change the source code without breaking existing functionality. This makes debugging much easier.

- test first, implement afterward
- forces you to work incrementally
- forces you to keep it simple!

### Unit Testing

`Unit testing` is the testing of individual software components in isolation from the rest of the system.

> Why are unit tests important?

When developing software, it is important to ensure that most if not all of the code being written is tested to verify the functionality of the code.

### JUnit

#### JUnit 5 Features

- requires Java 8, though it can test older Java versions
- allows using `lambdas` in assertions
- not an all-in-one library but a set of well-structured modules
- provides a completely new set of annotations
- a new feature called `Grouped Assertions` which allows the execution of a group of assertions and have failures reported together
- you can use `assertThrows` and `equalsThrows`.

#### Annotations

> How can JUnit annotations help with running our tests?

`Annotations` are used to support, identify, and execute test method features.

- `@BeforeAll`
- `@BeforeEach`
- `@AfterEach`
- `@AfterAll`
- `@Test`

#### Assertions

- assertTrue and assertFalse
- assertNotNull and assertNull
- assertThrows
- assertSame and assertNotSame
- assertEquals and assertNotEquals

#### Best Practices

- methods being tested should have one single purpose
- 1 assertion per test
- deterministic tests (result should be the same given the same input)

#### How to use

To use Junit add it as a dependency to `pom.xml`

```xml
<dependencies>
  <!-- https://mvnrepository.com/artifact/org.junit.jupiter/junit-jupiter-api -->
    <dependency>
      <groupId>org.junit.jupiter</groupId>
      <artifactId>junit-jupiter-api</artifactId>
      <version>5.10.0</version>
      <scope>test</scope>
    </dependency>
</dependencies>
```

Write Tests:

```java
// import JUnit
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.*;

// TestClass for fictional CheckList Class
public class ChecklistTest {

  private Checklist list = new Checklist();

  // use @BeforeEach annotation for task to do before each test
  @BeforeEach
  public void listSetUp() {
      list.createTask("do laundry");
  }

  // use @Test assertion for tests
  @Test
  public void test_createTask_fails_because_name_is_whitespace() {
    // use lambda expression to call method
    // use assertThrows to see if Exception is thrown
    assertThrows(IllegalArgumentException.class, () -> list.createTask(" "));
  }
}
```

### Mockito

> What is Mockito and why would we use it?

Mocking framework used for unit tests

Mockito records the interaction with mock and allows you to check if the mock object was used correctly, e.g. if a certain method has been called on the mock.

This allows you to implement behavior testing instead of only testing the result of method calls.

> What is a mock?

A `mock` object is a dummy implementation for an interface or a class.

About Mockito:

- uses annotations to identify its functionality, similar to JUnit
- `mock`: replacement object - behavior is stubbed unless we request real behavior
- `spy`: replacement object - behavior is real unless we request it is stubbed
- from the docs: "Real spies should be used carefully and occasionally, for example when dealing with legacy code."
- `stub`: replacement behavior

#### Creating Mocks

- `@InjectMocks` is used on the object being tested to specify what to inject with a mock
- `@Mock` to specify what should be mocked
- `MockitoAnnotations.openMocks()` is used to perform the injection
- Mockito will use any constructors available in the real object for injection, otherwise it will try using setters, and then finally it will try using fields

#### Stubbing

- `when()` is used to target an invocation
- `thenReturn()` is used to return dummy results
- `thenThrow()` is used to throw exceptions
- if a mock's method isn't stubbed, it will return default values (null, empty collection, 0, false, etc)
- with [`void` methods](https://www.baeldung.com/mockito-void-methods) use:
  - `doThrow()`
  - `doAnswer()`
  - `doNothing()`
  - `doCallRealMethod()`

#### Verify

- a mock will remember all method invocations on it for verification
- `times(x)` is used to verify a behavior was invoked x many times
- `never()` is used to verify a behavior was not invoked
- `atMostOnce()`, `atLeastOnce()`, `atMost(x)`, `atLeast(x)`

#### Example

```java
// import JUnit
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.*;
// import Mockito
import static org.mockito.Mockito.*;
import org.mockito.*;

public class
PetServiceTest {
  // specify which object to inject into
  @InjectMocks
  private PetService petService = new PetServiceImpl();

  // specify what to inject
  @Mock
  private PetDAO petDAOMock;

  @BeforeEach
  public void setUpTests() {
      // does actual injecting
      MockitoAnnotations.openMocks(this);
  }

    // test
  @Test
  public void test_getPetById_succeeds() {
      // arrange: create dummy info for dummy method to return
      Pet pet = new Pet(1, "Dobby", 3, "Dog", 1);
      when(petDAOMock.getPetById(1)).thenReturn(pet);

      // act: use actual implementation of object you are trying to test
      Pet petReturned = petService.getPetById(1);

      // assert
      assertEquals(pet, petReturned);
  }

@Test
  public void test_getAllPetsByVetId_calls_getAllPets_once() {
      // set up
      List<Pet> testList = new ArrayList<>();

      // stub
      when(petDAOMock.getAllPets()).thenReturn(testList);

      // just call it
      petService.getAllPetsByVetId(4);

      // verify(what obj, how many times).invocation()
      verify(petDAOMock, times(1)).getAllPets();

      // times(1) is the default, so same as
      verify(petDAOMock).getAllPets();

      verify(petDAOMock, atLeastOnce()).getAllPets();
  }
}

```
