
# `Spring Cloud Consul` for distributed configuration
> The `Consul Server` shares the respective configuration data to all the microservices during the `bootstrap phase`.

The `bootstrap context` gets loaded before the `application context`.

## Source
- [Spring Documentation](https://docs.spring.io/spring-cloud-consul/reference/config.html)

## Install `consul`
- install from: [consul](https://developer.hashicorp.com/consul)
- add to Path
- restart gitbash

Start consul with:
```bash
consul agent -server -bootstrap-expect=1 -data-dir=consul-data2 -ui -bind=192.168.254.79
```
- `-server` starts it as a server (not a client)
- `-bootstrap-expect-1` set it up to create one instance (not a cluster)
- `-data-dir` specifies the folder consul stores the config data
  - it will be created in the same folder where consul is
  - if does not exists consul will create it
  - if exists consul will use it the config data from here to start the consul server
- `-ui` sets consul up to run in a web ui mode
- `-bind` specifies the IP address of the host where the consule server should start (find out ip address with `ipconfig`)

To see consul running open browser to: `localhost:8500/ui`.

## Store Configuration Details in consul

- consule has a key-value store to store the configuration data
- consul stores config data in the file system
- supported formats are:
  - YAML
  - JSON
  - XML
- more specific config files have higher precedence and loaded first
  - config/App/dev - profile specific
  - config/App - application spedific
  - config/application - common config


### store common configuration
- go to consul ui (`localhost:8500/ui`)
- select `Key/Value` menu item (on left side panel)
- click `Create` button in top right corner
- enter file name in `Key or Folder` input area
- `config/application/data`
  - by default configuration data is stored in the `config` folder
  - `application` folder will store all common properties
  - `data` will be the name of the file we store the configuration data 

`config/applciation/data`
```yml
spring:
  datasource:
    username: root
    password: password
  jpa:
    hibernate:
      ddl-auto: update
```

### store microservice specific configuration
Create new `Key/Value` a file.
- `config/ownerMS/data`
- create new folder in the `config` folder
- new folder's name has to match the application name

`config/ownerMS/data`
```yml
spring:
  datasource:
    url: jdbc:mysql://localhost/owner
```

## Configure Consul in Microservice

Sources:
- [consul configuration](https://docs.spring.io/spring-cloud-consul/docs/current/reference/html/#spring-cloud-consul-config)

### 1. Add dependencies

`pom.xml`
```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-consul-config</artifactId>
</dependency>
```

### 2. Import Configuration Data

In `application.properties` add:
```bash
spring.config.import=optional:consul:
```
- will import configuration from the consul server
- removing the  `optional` prefix  will make consul config to fail if it cannot connect to the consul server
- will connect to default `Consul Agent` at `http://localhost:8500`
- to set host and port use syntax: `spring.config.import=optional:consul:myhost:8500` 

Remove properties moved to `Consul Server` from the  `application.properties` file.

### 3. Configure Consul Server

Create an `src/main/resources/application.yml` file:
```yml
spring:
  cloud:
    # configuring Cloud Config
    consul:
      config:
        # true enables Cloud Config
        enabled: true
        # sets the base folder for configuration
        # config is the default name
        prefix: config
        # sets the folder name used by all applications
        defaultContext: application
        # set the value of the separator
        # used to separate the profile name
        # in property sources with profiles
        profileSeparator: '::'
        # name of file config for specific microservice
        # is stored in the microsercice's name space
        # default is `data`
        data-key: data
        # configures consul server to resend config data
        # to the microservice at every 100ms
        watch:
          delay: 100
        # IMPORTANT will not work without setting format
        format: YAML
```




## Qustions
> Spring consul by deafault stores config data in ...?

In the file system.
