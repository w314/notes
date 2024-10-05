# Spring MS API GateWay

## Spring Cloud Gateway
- automatically load balances the requests
- provides automatic circuit breaker support
- hat to be a consul client

## Setting Up a  GateWay Server

### 1. Create new Spring Project

### 2. Add Dependencies

`pom.xml`
- spring-cloud-starter-gateway
- spring-boot-starter-actuator
- spring-cloud-starter-consul-discovery
- spring-cloud-netflix-hystrix

### Add Configuration

Create `/resources/bootstrap.yml`
```yml
server:
  port: 9000

spring:
  application:
    # name the gateway will register itself with the consul server
    name: GatewayMS
  cloud:
    consul:
      discovery:
        hostname: localhost
```
Also create `/resources/application.yml`
```yml
# enable discovery client
spring:
  cloud:
    gateway:
      discovery:
        locator:
          enabled: true
      # configures routes for the microservices
      routes:
        # name microservice
      - id: CallDetails
        # lb stands for load balanced
        # load balancing will be taken care of automatically
        uri: lb://CallDetailsMS
        predicates:
        - Path=/cutomers/*/calldetails
        # filters if needed
        filters:
        # set #of parts to strip fom urls
        # would transfrom /mock/customers -> /customers
        - StripPrefix=1
        # repeat for all microservices
```
- predicates uri:
    - should be a path like: 
    - `uri: http//localhost:9400`
    - or the load balanced service name like:
    - `uri: lb://PlanMs` 


## Configuration Examples

Gateway Server is running on port 8080 on localhost.

Base Configuration:
```yml
spring:
  cloud:
    gateway:
      discovery:
        locator:
          enabled: true
      routes:
      - id: CallDetails
        uri: lb://CallDetailsMS
```

`filter` configuration:
```yml
        predicates:
        - Path=/cutomers/*/calldetails
        filters:
        
        - StripPrefix=1
```
- `StripPrefix=1` sets the # of parts to strip fom urls
- would transfrom `/mock/customers` -> `/customers`

`Query` configuration:
```yml
routes:
  -id: CustomerMS 
   uri: lb://cust
   predicates: 
   -Path= /cust/**
   - Query= sports
```
Valid Routes:
- `http://localhost:8080/cust/foo?sports=hockey`
