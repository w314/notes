# ORM (Object Relational Mapping)
> Technique / design pattern which maps and object model with a relational model.

- maps:
    - java classes to tables
    - instance variables to columns of a table
    - objects to rows in a the table
- database independent 
    - as all databases provid esupport for ORM
    - make appliction protable, independent of the underlying database


To use `ORM` in a java application the `Java Persistence API (JPA)` specification is used.

### Object Relaional Impedance Mismatch

 

> `Object Relaional Impedance Mismatch`is a paradigm mistmatch between object and relational model.

 

Problems arising from Object Relational Impdance Mismatch:

- **problem of granularity**: data can be represented in two classes in java but just one table in the database

- **problem of inheritance**: there is no inheritance in db

- **problem of identity**: equality is defined differently for table rows (same primary key) and java objecst (result of the equals() method)

- **problem of association**: different ways of describing association refernce variables vs foreign key, plus no way to store info about the directionality of relationships in tables

- **problem of data navigation**:

 

### Solution : ORM

- provides a way to map Java objects to tables

- allows automatic conversion between object and relational models

 

ORM Maps

- Java classes to tables

- instance variables to table columns

- objects to table rows

 

To use ORM in Java Application `Java Persistence API (JPA)` is used. It has many implementation, we use `Hibernate`.

 

#### Spring ORM Advantages

The DAO layer has many dependencies (EntityManager instance, JDBC DataSource instance, transaction managers... ) Spring dependency injection makes it easy to replace these dependencies.

- easy testing (easily can change dependencies and test without deploying to a server)

- common data access exceptions (DAO class annotated with @Repository always throws `DataAccessExeption` independent from the persistent layer used)

- automatic resource management through dependency injection

- easy transaction management (Spring support transaction management)

 

## JPA (Java Persistence API)

 

### Map Classes to Tables

 

Classes that are mapped to tables are `Entity Classes`, their instances represent a row in the table.

 

Entity classes are described in the `jakarta.persistence` package.

 

```java

// identifies class as entity class to matched to a db table
@Entity
// only needed if you do not want to use the class name as table name
@Table(name="customer")
public class Customer {

    // every object of the entity class has to have field that uniquely identifies it
    @Id
    // @Column is only needed if you want differetn column name than the attribute name
    @Column(name="customer_id", nullable=false)
    private Integer customerId;

    @Column(name="customer_name", nullable=false, length=50)
    private String customerName;

    //rest of the code

}

```

- `@Transient` specifies the attributes which are not stored

- in `SpringPhysicalNamingStrategy` camel case is replaced by underscores firstName -> first_name

 

#### Best Practice

 

- do override the `equals()` and `.hashCode()` methods

- one table should be associated with one entity

 

#### Persist Enums

 

To persist enum use the `@Enumerated` annotation:

```java

public enum CustomerType{

    SILVER,GOLD,PLATINUM;

}

 

@Entity

public class Customer {

    @Id

    @Column(name="customer_id")

    private Integer customerId;

    @Enumerated(EnumType.STRING)

    private CustomerType customerType;

    //getters and setters

}

```

 

The `EnumType` property specifies how the enum should be persisted in the database.

- with `EnumType.STRING` SILVER would be persisted as SILVER

- with `EnumType.ORDINAL` SILVER would be persisted as 0

- the default is  **EnumType.ORDINAL**

 

### Perform CRUD operations

`EntityManager` can be injected with `@PersistenceContext` OR `@Autowired`.

 

Add new customer example:

``` java

@Repository

public class CustomerRepositoryImpl implements CustomerRepository{

     @PersistenceContext

     private EntityManager entityManager;

     

     //add customer details

     public void addCustomer(CustomerDTO customerDTO) {

        Customer entity=new Customer();

        entity.setCustomerId(customerDTO.getCustomerId());

        entity.setName(customerDTO.getName());

        entityManager.persist(entity);

    }

```

 

### Transaction Management

 

Important for database consistency and integrity.

 

#### Programmatic Transaction Management NOT PREFERRED

 

```java

Transaction transaction = entityManager.getTransaction()                  

try{  

   transaction.begin();                  

   // business logic                  

   transaction.commit();  

}                  

catch(Exception exception){                    

   transaction.rollback();  

   throw exception;                  

}

```

Has to be added to each method. As is means repeated code it is not preferred.

 

#### Declarative Transaction Management

 

- Preferred as code to manage transactions is separated from business logic.

- Uses the `@Transactional` annotation

 

##### `@Transactional` Annotation

- when used at **class level**, all public methods become transaction

- can be used at **method level**

- if used on both class and method level, the method level annotation overrides the class level

- good practice to use with Service classes

 

##### Annotation Attributes

Attributes with default values:

- `isolation` = DEFAULT

- `propagation` = REQUIRED

- `timeout` = TIMEOUT_DEFAULT

- `readOnly` = false

- `rollbackFor` = RuntimeException or its subclasses

- `noRollbackFor` = Exception or its subclasses

 

### Persistence Layer Best Practices

- manage transactions only in service layer

- abstract persistence layer from service layer

    - no business logic in persistence layer

    - makes changing databases easy



