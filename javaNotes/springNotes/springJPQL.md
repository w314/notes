## JPQL (Java Persistent Query Language)

- To create queries not included in the repository methods.

- JPA implementations translate JPQL queries to SQL using query translator.

 

### Query Interface

 

JPA provides the `Query Interface` to create and execute JPQL queries.

 

To create a `Query Interface` object use the `EntityManager`interface's `createQuery()` method:

```java

Query query = EntityManager.createQuery("SELECT c FROM Customer c");

```

- the parameter is the JPQL query

 

#### Query Interface Methods

 

- `List getResultList()`

    - returns a list of results

    - throws `IllegalStateException` if called for update or delete queries

- `Intger executeUpdate()`

    - executes update and delete queries

    - returns the number of rows affected  

    - throws `IllegalStateException` if called for select queries

- `Object getSingleResult()`

    - returns a single results

    - throws `NoResultException` if there is no result

    - throws `NonUniqueResultException` if there are several results

    - throws `IllegalStateException` if called for update or delete queries

 

#### Select Query

 

```java

Query query = entityManager.createQuery("SELECT c FROM Customer c");

List<Customer> customers = query.getResultList();

```

- c is alias for Customer

- `DISTINCT` can be used for unique results

 

To get only customer names:

```java

Query query = entityManager.createQuery("SELECT c.customerName FROM Customer c");

List<String> customers = query.getResultList();

```

 

When returning several attributes:

```java

Query query = entityManager.createQuery("SELECT c.customerName, c.dateOfBirth FROM Customer c");

List<Object[]> customers = query.getResultList();

```

- return type is List<Object[]>

- can use `getResultList().subList()

BEST PRACTICE to only ask for needed attributes in select.

 

#### WHERE Clause

 

```java

SELECT c FROM Customer c WHERE c.customerId = 1002;

```

 

Using named parameters - `:`

```java

List<Customer> getCustomerDetails(Integer customerId){

     Query query = entityManager.createQuery("SELECT c FROM Customer c WHERE c.customerId = :customerId");

     query.setParmeter("customerId",customerId);

     List results = query.getResultList();

}

````

 

Using positional parameters - `?1`

```java

List<Customer> getCustomerDetails(Integer customerId){

     Query query = entityManager.createQuery("SELECT c FROM Customer c WHERE c.customerId = ?1");

     query.setParmeter(1,customerId);

     List results = query.getResultList();

}

```

 

WHERE Clause Operators

- `=`

- `!=`

- `>`, `>=`, `<`, `<=`

- `BETWEEN` only the from is included

- `LIKE` - starting with R: 'R%'

- `IS NULL`

- `IN` or `NOT IN`

 

`IS EMPTY`or `IS NOT EMPTY`

```java

SELECT c FROM Customer c WHERE c.loans IS EMPTY

```

returns customer without any loans

 

`SIZE`

```java

SELECT c FROM Customer c WHERE SIZE(c.loans) > 2

```

 

#### Aggregate Functions

Same ones as in sql.

```java

SELECT AVG(a.balance) FROM Account a

```

 

#### String Functions

- `CONCAT`

- `LOCATE(String s1, String s2)`

    - if not found returns 0

    - by default starts at the beginning

- `SUBSTRING(String str, int start, int length)`

    - last parameter is length

- `TRIM(String s, int start, int length)`

- `LOWER`

- `UPPER`

 

#### Grouping and Ordering

 

```java

SELECT c.city, COUNT(c) FROM Customer c GROUP BY c.city HAVING c.city IN ('Seatle','Vancouver') ORDER BY c.city ASC

```

 

#### Update Queries

 

```java

UPDATE Customer c SET c.city = 'Seatle' where c.customerId = 1002;

```

 

#### Delete Queries

 

```java

DELETE FROM Account a WHERE a.status = 'INACTIVE'

```

 

To execute:

```java

Query query = entityManager.createQuery("DELETE FROM Account a WHERE a.status = 'INACTIVE'");

int updatedEntities = query.executeUpdate();

```

 

### Createing queries by method name

To allow for custom queries not provided by `CrudRepository` you can add methods to your Repository Interface, and Spring Data automatically generates the JPQL query based on the name of the method.

 

### @Query

For creating complex queries.

 

#### Select with @Query

Add method to your Repository interface:

```java

public interface CustomerRepository extends CrudRepository<Customer, Integer> {

    //JPQL query

    @Query("SELECT c.name FROM Customer c WHERE c.emailId = :emailId")

    // method to find Name by email

    String findNameByEmailId(@Param("emailId") String emailId);

 

    // OR

 

    public interface CustomerRepository extends CrudRepository<Customer, Integer> {

        @Query("SELECT c.name FROM Customer c WHERE c.emailId = ?1")

        String findNameByEmailId(String emailId);

    }

 

}

```

 

#### Insert, Update & Delete queries

 

Must use:

- @Query

- @Modifying

- @Transactional

 

```java

public interface CustomerRespository extends CrudRepository<Customer, Integer> {

    @Query("UPDATE Customer c SET c.emailId = :emailId WHERE c.customerId = :customerId")

    @Modifying

    @Transactional

    Integer updateCustomerEmailId(@Param("emailId") String updateCustomerByEmailId, @Param("customerId") Integer customerId);

}

```

`@Modifying` marks the method for non-select query

 

### @NamedQuery

 

To set up custom queries you can:

```java

@Entity

@Table(name="customer")

@NamedQuery(name="Customer.findNameByEmailId", query="SELECT c.name FROM Customer c WHERE c.emailId = :emailId")

public class Customer {

    @Id

    private Integer customerId;

    private String emailId;

    private String name;

    private LocalDate dateOfBirth;

    @Enumerated(value=EnumType.STRING)

    private CustomerType customerType;

    // ....

}

```

The `name` attribute should be ClassName.methodName.

 

In your repository interface add the method:

```java

public interface CustomerRespository extends CrudRepository<Customer, Integer>{

    String findNameByEmailId(@Param("emailId") String emailId);

}

```

 

### JPARepository