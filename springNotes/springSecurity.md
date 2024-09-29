spring, security

# Spring Security

 

- open-source

- platform independent

- uses declarative programming

- annotation based

 

Services Covered:

- Authentication

    - basic authentication with default login/HTTP basic form

    - authentication against database

    - secure password storage

    - authentication against LDAP

- Authorization

    - role-based access

    - restricting URL access

    - method level security

    - page level security

- Session Management

- HTTPS channel security

- Remember Me Service

 

### How It Works

- It is based on a chain of filters for authentication and authorization.

- Each filter is applied to every request for authentication and authorization

- if the request does not have proper credentials

    - it is rejected

    - exception is thrown

 

## Important Filters

 

`UsernamePasswordAuthenticationFilter`

- authenticates

 

`AnonymusAuthenticationFilter`

- if there are no authentication credentials this filter creates an anonymus user

- these users are allowed to access API's which does not require authentication

 

`ExceptionTranslationFilter`

- translates security exceptions to HTTP responses

 

`FilterSecurityInterceptor`

- performs authorizations

 

## HTTP Basic Authentication

 

There are multiple approches for authentication and authorization in Spring Security one of them is HTTP basic authentication.

 

Basic steps of HTTP Basic Authentication:

1. client send request

2. server requires authentication credentials

3. client encodes username & password

4. client send encoded credentials

5. server decodes and verifies credentials

6. server send requested resource

 

Features of HTTP Basic Authentication

- does not require login page

- useful for web services interacting for each other

- no need for sessions to store credentials

- each request is treated independently which promotes scalability

- default authentication approach if Spring Security is enabled




## Using Spring Security

 

Include dependency in `pom.xml`

```xml

<dependency>

     <groupId>org.springframework.boot</groupId>

     <artifactId>spring-boot-starter-security</artifactId>

</dependency>

```

 

When included Spring Boot configures default security configuration for the whole application.

 

It will include features:

- all requests are authenticated using HTTP Basic Authentication

- one user is generated

    - username will be `user`

- default password

    - generated during application start

    - can be seen in the console log:

    - Using generated security password: 48bf...

- no roles are assigned to the user

 

<br>

You can define user details in `application.properties`:

 

```bash

spring.security.user.name=

spring.security.user.password=

spring.security.user.roles=

```

 

## Setting Up Custom Configuration

 

Credentials can be stored:

- database

- active directory like LDAP

- in-memory data source

 

The example below uses in-memory datasource.

 

### Create a security configuration file:

```java

@Configuration

@EnableWebSecurity

public class SecurityConfig {

    // ...

}

```

- `@Configuration` marks it as a Configuration Class

- `@EnableWebSecurity` enables Spring Security's web security support

 

### Implement Authentication

 

#### Use Password Encrypter

 

```java

@Bean

PasswordEncoder passwordEncoder() {

    return new BCryptPasswordEncoder();

}

```

#### Create method `userDetailsService()`

```java

@Bean

public InMemoryUserDetailsManager userDetailsService() {

    UserDetails user = User.withUsername("smith").password(passwordEncoder().encode("smith123")).roles("ADMIN")

            .build();

    UserDetails admin = User.withUsername("tim").password(passwordEncoder().encode("tim123")).roles("USER").build();

    return new InMemoryUserDetailsManager(user, admin);

}

```

- returns an instance of `InMemoryUserDetails Class`

- responsible for providing user details for authentication

 

### Authorization

 

Setup filter chain:

```java

@Bean

public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {

 

    // setup URI to be checked

    String requestMatcher = "/infybank/customers/**";

   

    // set authorization rules

    http.httpBasic(Customizer.withDefaults()).authorizeHttpRequests(

            (authorize) -> authorize.requestMatchers(HttpMethod.GET, requestMatcher).permitAll()

                    .requestMatchers(HttpMethod.PUT, requestMatcher).hasAnyRole("ADMIN", "USER")

                    .requestMatchers(HttpMethod.POST, requestMatcher).hasRole("ADMIN")

                    .requestMatchers(HttpMethod.DELETE, requestMatcher).hasRole("ADMIN").anyRequest()

                    .authenticated());

 

    // disable cross site request forgery to allow method other than GET

    http.csrf(csrf -> csrf.disable());

 

    // configure cors

    http.cors(cors -> cors.configurationSource(request -> {

        CorsConfiguration config = new CorsConfiguration().applyPermitDefaultValues();

        config.addAllowedMethod(HttpMethod.PUT);

        config.addAllowedMethod(HttpMethod.DELETE);

        return config;

    }));

 

    // return SecurityFilterChain object

    return http.build();

}

```

 

- The URI to be protected is mentioned using `requestMatchers()` method. In URI "/api/customers/**", `**` means any value after /api/customer

- `httpBasic()` specifies that HTTP basic authentication has to be used

- `permitAll()`

- `anyRequest().authenticated()` means any request mapped to this URI will be authenticated

- `cors()` method of  HttpSecurity object configures Cross-Origin Resource Sharing (CORS) settings. In example, the configuration supports PUT and DELETE methods.

 

#### CSRF (Cross Site Request Forgery)

The Spring security by default enables CSRF(Cross Site Request Forgery) protection. Because of this you can access only GET endpoints. For accessing PUT, POST and DELETE endpoints, you have to disable the CSRF protection. So this is disabled usign the below code:

 

```java

http.csrf(csrf -> csrf.disable());

```

- usually disabled if API is consumed by non-browser based clients

- other solution is to send csrf tokens

 

# Spring Data

 

## Srping Data JPA

 

## Custom Queries in Spring DATA




### Using `@Query`

 

In repository interface

```java

public interface CustomerRepository extends CrudRepository<Customer, Integer> {

    @Query("SELECT c.name FROM Customer c WHERE c.emailId = :emailID")

    String findNameByEmailId(@Param("emailId") String emailId);

 

    @Query("UPDATE Customer c SET c.emailId = :emailId WHERE c.customerId = :customerId")

    @Modifying

    @Transactional

    Integer updateCustomerEmailId(@Param("emailId") String emailId, @Param("customerId") String customerId);

 

    @Query("DELETE FROM Customer c WHERE c.customerId = :customerId");

    @Modifying

    @Transactional

    Integer deleteCustomerByCustomerId(@Param("customerId") Integer customerId);

 

}

```

- for UPDATE and DELETE queries use:

    - @Modifying

    - @Transactional

 

### Using `@NamedQuery`

 

In entity class:

```java

@Entity

@Table(name = "customer")

@NamedQuery(

    name="Customer.findNameByEmailId",

    query="SELECT c.name FROM Customer c WHERE c.emailId = :emailId")

public class Customer {

    @Id

    private Integer customerId;

    private String name;

    private String emailId;

}

```

 

In repostiroy interface:

```java

public interface CustomerRepository extends CrudRepository<Customer, Integer> {

    String findNameByEmailId(@Param("emailId") String emailId);

}

 

 

# Srping Security

> **Athentication**: verifying the identity of the user.

> **Authorization**: restricting access.

Dependency in `pom.xml`
```java
<dependency>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

