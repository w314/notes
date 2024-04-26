models, java, spring data, spring mvc

# How to Create Models

For models to be created in database, your main class has to have the @EntityScan tag:
```java
@EntityScan("com.wp.ERS.models")
public class ErsApplication {

	public static void main(String[] args) {
		SpringApplication.run(ErsApplication.class, args);
	}

}
```

## Model Sceleton
```java
@Entity // marks class as a table in our database
@Table(name = "reimbursements") // sets table name
@Component // marks the class as a Bean
public class Reimbursement {
}
```

## Create Primary Keys

Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'entityManagerFactory' defined in class path resource [org/springframework/boot/autoconfigure/orm/jpa/HibernateJpaConfiguration.class]: [PersistenceUnit: default] Unable to build Hibernate SessionFactory; nested exception is org.hibernate.MappingException: Column 'id' is duplicated in mapping for entity 'com.wp.ERS.models.Reimbursement' (use '@Column(insertable=false, updatable=false)' when mapping multiple properties to the same column)

## Create ENUM fields
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

## Set Constrains
```java
@Column(nullable = false, unique = true)
private String username; 
```

## set up One to Many relationships
```java
// on the MANY side
    @ManyToOne 
    @JoinColumn(name = "id")  // name of primary key field in Employee Class
    private Employee employee;


// on the ONE side

```
