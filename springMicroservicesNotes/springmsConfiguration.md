# Configuratoin
To avoid having the same configuration sitting in all the microservices, we set up a configuration server to store the common configurations.

Possible Solutions
- Spring Cloud Consul
- Zookeeper
- Spring Cloud Config

## `Consul`
> A service networking solution to automate configuration.

- consul server shared configuration with the microservices during the `bootstrap phase`

 

1. create directory in cloud

2. add configuration file for each MS

3. name of config file should match spring.application.name: `appName.properties`

4 add one central file named `application.properties`

 

4. create new spring boot project for a Configuration Server

5. set its application.properties

 

```bash

 

```

5. Configurations are taken only once at the time of startup. Need to add actuator dependency with @RefreshScope annotation on the bean which is using the property also POST request to the /refresh endpoint

 

6. When the properties file is accessed through config server endpoint, the properties are served in JSON format.

 

7. create `bootstrap.properties`

```bash

spring.cloud.config.uri=http://localhost:1111

```

## info

 

1.

`spring.cloud.config.fail-fast=true`

Makes sure, that If the cloud-config server is down, then the client will throw an error at runtime not during startup so the config server has to start first then Microservices are allowed to start.

 

2.

A microservice has both local as well cloud config. The **local overrides** the cloud one.

 

3.

Which of the below will take priority in cloud config?

- application.yml

- application.properties

> .yml config file has higher priority than properties files

 

4.

 

If the config server fails, the local configuration will be used.

 

TRUE - If the cloud config server is unavailable, it will use the properties files in the individual applications as a fallback

 

(me: how if you put config in local files and that overrides)

 

# Load Balancing with Ribbon

 

Our service has to contact an other microservice. Due to high need several servers run the microservice we need to connect to.

 

We set up ribbon for software load balancing (instead of using a hardware load balancer between our MS and the other one)

 

To set up ribbon we have to do the following changes:

 

## Set up Ribbon Load Balancer

 

### 1. Add Dependency

`pom.xml`

```bash

<dependency>

            <groupId>org.springframework.cloud</groupId>

            <artifactId>spring-cloud-starter-netflix-ribbon</artifactId>

</dependency>

```

 

### 2. Create configuration class

- create class on same level in directory as application file

 

`CustomerConfig.java`

```java

@Configuration

public class CustomerConfig {

 

    // method will return a load balanced rest template object

    // to be used when making http requests

    @Bean @LoadBalanced

    RestTemplate restTemplate() {

        return new RestTemplate();

    }

}

```

 

### 3. Add instances to balance

In `bootstrap.properties` OR in `application.properties`

```bash

# disable eureka

custribbon.ribon.eureka.enabled=false

# set list of servers (no space after comma)

# choose a name for list of server, here it is: custribbon

custribbon.ribbon.listOfServers=http://localhost:8300,http://localhost:8301

```

 

### 4. Use Load Balanced Rest Template for http requests

- add @RibbonClient annotation

- autowire load balanced rest template

- use load balanced rest template for http calls

- use server names from config file for path in http calls

 

`CustomerController.java`

```java

// add annotation @RibbonClient with name of list of servers

@RibbonClient(name="custribbon")

public class CustomerController {

 

    // autowire created load balanced rest template

    @Autowired

    RestTemplate template;

 

    // use this template for http calls

    // instead of new RestTemplate().getForObject(planUri, Plan.class)

    // -> use template instead of new RestTemplate()

    // -> use ribbon name instead of planUri

    Plan plan = template.getForObject("http://custribbon/customers"+planId, Plan.class);

}

```

 

### 5. Configure Ribbon

- by default ribbon uses the `NoOpPing` strategy and does not check if the service is up before calling it.

    - `iping` strategy would stop pinging after a while

- by default it uses round robing balancing strategy

- to configure robin use: `<clientName>.<nameSpace>.<propertyName>=<value>

`

```bash

custribbon.default.NFLoadBalancerRuleClassName=com.netflix.loadbalancer.RandomRule

```

 

# Service Discovery with Eureka

 

## Setup Service Discovery withe Eureka

 

### 1. Create Eureka server

#### 1.1 create new spring boot project

#### 1.2 add dependecies

`pom.xml`

```bash

<dependencyManagement>

        <dependencies>

            <dependency>

                <groupId>org.springframework.cloud</groupId>

                <artifactId>spring-cloud-dependencies</artifactId>

                <version>Greenwich.RELEASE</version>

                <type>pom</type>

                <scope>import</scope>

            </dependency>

        </dependencies>

</dependencyManagement>

   

<dependency>

            <groupId>org.springframework.cloud</groupId>

            <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>

</dependency>

```

 

#### 1.3 add configuration for server

`application.properties`

```bash

spring.application.name=Eureka1

server.port=5555

 

# as we are running only 1 erueka service we do not need these

# they are only for running a cluster of eureka servers

eureka.client.fetch-registry=false

eureka.client.register-with-eureka=false

 

# contact information to eureka service

# as eureka is also an eureka client? instance?  we add this here

eureka.client.service-url.defaultZone=http://localhost:5555/eureka

```

 

#### 1.4 add @EnableEurekaServer annotation to app file

`MyEurekaServer.java`

```java

@SpringBootApplication

@EnableEurekaServer

public class MyEurekaServer {}

```

 

### 2. Add Service Registry Server to commin git config file

```bash

# contact information to eureka server

eureka.client.service-url.defaultZone=http://localhost:5555/eureka

```

 

### 3. Setup MicroServices

 

#### 3.1 add dependencies

`pom.xml`

```bash

<dependency>

            <groupId>org.springframework.cloud</groupId>

            <artifactId>spring-cloud-starter-ribbon</artifactId>

</dependency>

```

 

### 3.2 add @EnableDiscoveryClient in application file

Registers service with Eureka Server Registry.

 

### 3.3 modify controller class

- autowire DiscoveryClient client

    - use the one from cloud.client.discoveryClient (not netflix)

-

 

```java

@RestController

@EnableAutoConfiguration

public class CustomerController{

 

    // autowire DiscoveryClient

    @Autowired

    DiscoveryClient client;

 

// get service instances from dicovery client

// we provide the name of the service which instances we are looking for

List<ServiceInstance> friendInstances = client.getInstances("FriendFamilyMS");

// get one instance form the list

ServiceInstance friendInstance = friendInstances.get(0);

// get uri of instance

URI friendUri = friendInstance.getUri();

 

// use obtained uri in http requests

List<Friend> friends = new RestTemplate().getForObject(friendUri+"/customers/"+phoneNo, List.class);

 

}

```

 

## About Eureka

### `@EnableDiscoveryClient`Annotation

    - makes an application an **Eureka instance**

    - as every application registered with Eureka is a Eureka instance

    - it also makes it an **Eureka client**

    - as it can get details about other services

 

### `register-with-eureka=true` property

- by default is set to true

- registers the app with eureka

- app will send heartbeat to eureka by default every 30 sec

- app will get deregistered if no heartbeats stop

 

### `fetch-registry` property

- will fetch registry at app start-up

- will cashe it

- will check for any changes by default every 30 sec

- only updates changed information

 

### Eureka Clusters

- Eureka server is also a client

- can register itself with other Eureka servers

- an Eureka cluster can be formed

- if only 1 Eureka server is run set the following properties to false

    - eureka.client.fetch-registry=false

    - eureka.client.register-with-eureka=false

 

### Discovery Client

- service endpoint

- returns an enum of all ServiceInstance instances of the registered clients

- endpoint address: `http://{eureka-host}:{eureka-port}/{eureka}/apps/{spring-application-name}

 

## Ribbon with Eureka

- NO need to autowire DiscoveryClient

- do autowire RestTemplate

- do NOT use ribbon names

- USE microservice names registered with Eureka in path

 

### 1. remove ribbon from properties

 

`application.properties`

```bash

string.application.name=CustomerMS

server.port=8200

# REMOVE BELOW

# by default ribbon is always enabled with eureke, so remove

# custribbon.ribbon.eureka.enabled=false

# as we'll get the list of server from eureka also remove

# custribbon.ribbon.listOfServers=http://localhost:8300,http://localhost:8301

```

 

### 2. update controller class

- autewire RestTemplate

- remove autowired DiscoveryClient, load balanced Rest Template will provide list of servers

- use microservice name in path for Http requests

 

### 3. add unique instance id property

Intances have to have **unique** instance id's otherwise they will overwrite each other in Eureka registry

 

Add id in microservise property file in git:

`FriendMS.properties`

```bash

spring.datasource.url=jdbc:mysql://localhost/infyfriends

# add unique eureka instance id

eureka.instance.instance-id=${spring.cloud.client.hostname}:${spring.application.name}:${spring.application.instance_id:${random.value}}

```

 

 

