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
# setting up required routes here
      routes:
        # set microservice details
      - id: CallDetails
        # lb stands for load balanced
        # load balancing will be taken care of automatically
        uri: lb://CallDetailsMS
        predicates:
        - Path=/cutomers/*/calldetails
        # repeat for all microservices

spring:
  cloud:
    gateway:
      mvc:
        routes:
        - id: nameRoot
          uri: https://nameservice
          predicates:
          - Path=/name/**
          filters:
          # number of parts in the path to strip
          # /name/blue/red -> /red (with using 2)
          - StripPrefix=2
```
- predicates uri:
    - should be a path like 
    - `uri: http//localhost:9400`
    - or the load balanced service name like 
    - `uri: lb//PlanMs` 


