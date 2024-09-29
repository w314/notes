# Rest Template
Making HTTP requests from Spring Boot

```java
// get customer from customer API
String url = "localhost/customer";

// takes url, and responseType as parameters
Customer customer = new RestTemplate().getForObject(url, Customer.class);
```
- response has to be `responseType.class`
