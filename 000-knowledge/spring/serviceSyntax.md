java, spring, services

# Service Syntax

```java
@Service // make it a bean
public class EmployeeService {
    
    // insert dao dependency
    // employeeDAO is an interface it cannot be instantiated
    // it has to be inserted as a dependency
    @Autowired
    private EmployeeDAO employeeDAO; 
    
}
```