# Setup Spring Microservices
- how to setup microservices to use consul for service discovery
- how to setup gateway server

## Separate Monolith to Microservices
- use separate databases
    - remove foreign keys
- use `RestTemplate` to make API calls to other microservices (only temporary solution)


## Setup Centralized Configuation & Service Discovery

### 1. Start `Consul`

```bash
Start consul with:
```bash
consul agent -server -bootstrap-expect=1 -data-dir=consul-data2 -ui -bind=127.0.0.1
```
- `-server` starts it as a server (not a client)
- `-bootstrap-expect-1` set it up to create one instance (not a cluster)
- `-data-dir` specifies the data directory, it will be created in the same folder where consul is
- `-ui` sets consul up to run in a web ui mode
- `-bind` specifies the IP address of the host where the consule server should start (find out ip address with `ipconfig`)

To see consul running open browser to: `localhost:8500/ui`.

### 2. Add configuartion to consul

- open `Consul` on `localhost:8500`
- go to `Key/Values`

#### For Microservices Common Config
- click `Create`
- For `Key or Folder` enter:
- `config/application/data`
- for values enter:
```yml
spring:
  datasource:
    username: root
    password: password
```
- make sure that `YAML` format is selected
- save

#### For Microservice Specific Config
- Create file under `config/<microservice-name>/data`
- microservice name should match spring.application.name
- enter values:
```yml
server:
  port: 8100
spring:
  datasource:
    url: jdbc:mysql://localhost/owner
```
- make sure that `YAML` format is selected
- save


### 3. Configure Microservices

In `resources/application.properties`:
```bash
# needed for centralized configuration with consul
spring.config.import=optional:consul:
```

Create `resources/application.yml` with:
```yml
spring:
  application:
    # should be the same name used for
    # microservice specific config in consul
    name: petMS
  cloud:
    # sets up service discovery
    consul:
      discovery:
        # hostname of consul
        hostname: localhost
      config:
        enabled: true
        # sets base directory for configuration
        prefixes: config
        # sets directory for common configuation
        defaultContext: application
        format: YAML
```

### Create Gateway Server

#### Setup Config Data on Consul

- Under `Key/Values`
- Create `config/gateway/data`
```yml
server:
  port: 8484
```

### Configure Gateway
`application.yml`
```yml
spring:
  cloud:
    gateway:
      dicovery:
        locator:
          enabled: true
      routes:
        - id: petMs
          uri: lb://petMS
          predicates:
            - Path=/pets, /pets/**
```



## Errors Encountered

Description	Resource	Path	Location	Type
cvc-elt.1.a: Cannot find the declaration of element 'project'. [cvc-elt.1.a]	pom.xml	/gateway	line 2	Language Servers

Solution: use https instead of http in urls in `<project>`


## Gateway

TO register

`application.yml`
```yml
# consule would show port, but spring suit would say unknown port
server:
  port: 8484
spring:
  application:
    name: mock-gateway
  cloud:
    consul:
      discovery:
        hostname: localhost
```

Gateway Dependencies (cloud version 2021.0.5)
- spring-boot-starter-actuator
- spring-cloud-starter-consul-discovery
- spring-boot-starter-test
- 