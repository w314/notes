dao, java, spring boot, spring, interface

For daos to be able to injected the main class has to have the `@ComponentScan()` annotation

```java
@ComponentScan("com.wp.ERS")
public class ErsApplication {

	public static void main(String[] args) {
		SpringApplication.run(ErsApplication.class, args);
	}
}
```


- create daos package
- create dao interfaces

```java
@Repository // maked dao a bean
// dao extends JpaRepository to perform CRUD operations on the Employee entity
// in <> are the Model name and the type of the primary key
public interface EmployeeDAO extends JpaRepository<Employee, Integer> {
}
```
The Spring Data JPA automatically generates the implementation of the DAO interface  based on conventions and provides a wide range of database operations out of the box, reducing the need for boilerplate code.