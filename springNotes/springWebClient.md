spring boot, java, webclient

# WebClient
> The WebClient class of Spring is for making HTTP requests.

 Dependency in `pom.xml`
 ```xml
 <dependency>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-starter-webflux</artifactId>
</dependency> 
```

## How to Use

1. Create Web Client Instance

```java
WebClient webClient = WebClient.create();
```

2. Send HTTP Request

```java
Mono<CustomerDTO> customerDTOMono = webClient.get()
   .uri("http://localhost:8080/customers/{customerId}")
   .retrieve()
   .bodyToMono(CustomerDTO.class);
```
- `.get()` specifies the HTTP method used
- `.uri()` sets the URL
- `.retrieve()` retrieves the method
- `.bodyToMono()` converts response to `Mono` object

3. Convert Mono Object to a blocking object

```java
CustomerDTO customerDTO = customerDTOMono.block();
```

### POST

```java
public void addCustomer(CustomerDTO customer) {
        String url = "http://localhost:8765/infybank/customers";
        WebClient webClient = WebClient.create();
        String response = webClient.post().uri(url).bodyValue(customer).retrieve().bodyToMono(String.class).block();
        LOGGER.info(response);
        LOGGER.info("\n");
    }                 
```
- `.bodyValue()` sets the body of the request

### PUT

```java
public void updateCustomer(CustomerDTO customerDTO) {
        String url = "http://localhost:8765/infybank/customers/{customerId}";
        WebClient webClient = WebClient.create();
        webClient.put().uri(url, customerDTO.getCustomerId()).bodyValue(customerDTO).retrieve();
        LOGGER.info("Customer updated successfully");
        LOGGER.info("\n");
    }
```

### DELETE

```java
@SuppressWarnings("deprecation")
public void deleteCustomer(Integer customerId) {
String url = "http://localhost:8765/infybank/customers/{customerId}";
WebClient webClient = WebClient.create();
webClient.delete().uri(url, customerId).exchange().subscribe(response -> {
if (response.statusCode().value() == 200) {
LOGGER.info("Customer deleted successfully");
} else {
LOGGER.error("Failed to delete customer");
}
});
}
```
- `.exchange()` retrieves the response like `.retrieve()` but gives more control to access the response
- `.subscribe()` handles the response
    - first argument is a function to handle the response
    