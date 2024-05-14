models, java, spring data, spring mvc

# Spring Boot Syntax

## Application

```java
@EntityScan("com.wp.ers.models") // tells Spring to look for DB entities in that package
@ComponentScan("com.wp.ers") // tells Spring to look for beans
@EnableJpaRepositories("com.wp.repositories") // tells Spring to look for repositories in that package
@SpringBootApplication
public class ErsApplication {

	public static void main(String[] args) {
		SpringApplication.run(ErsApplication.class, args);
	}

}
```


## Models
### Model Skeleton
```java
@Entity // marks class as a table in our database
@Table(name = "reimbursements") // sets table name
@Component // marks the class as a Bean
public class Reimbursement {


}
```
### Create ENUM fields
```java
public class Reimbursement {
    
    // create enum
    enum Status {
        pending,
        approved
    }

    // give field enum type
    @Enumerated(EnumType.STRING)
    private Status status;
}
```

### Set Constrains
```java
@Column(nullable = false, unique = true)
private String username; 
```

### Set One to Many relationships
```java
// on the MANY side
    @ManyToOne 
    @JoinColumn(name = "id")  // name of primary key field in Employee Class
    private Employee employee;


// on the ONE side

```
