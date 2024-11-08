# Rest Template
> Used for making HTTP requests from Spring Boot application.

Blocking. See `springNotes/springClients.md`

```java
// get customer from customer API
String url = "localhost/customer";

// takes url, and responseType as parameters
Customer customer = new RestTemplate().getForObject(url, Customer.class);
```
- response has to be `responseType.class`
