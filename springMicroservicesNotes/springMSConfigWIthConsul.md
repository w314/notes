
# Spring Configuration

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

Consule has a key-value store to store the configuration data.
- consul stores config data in the file system
- go to consul ui (`localhost:8500/ui`)
- select `Key/Value` menu item (on left side panel)
- enter config information
```yml
spring:
  cloud:
    consul:
      config:
        # specifies the directory with common config
        default-context: application
        # name of file config for specific microservice
        # is stored in the microsercice's name space
        data-key: service
        # configures consul server to resend config data
        # to the microservice at every 100ms
        watch:
          delay: 100
```
- supported formats are:
  - YAML
  - JSON
  - XML
- more specific config files have higher precedence and loaded first
  - config/App/dev - profile specific
  - config/App - application spedific
  - config/application - common config

## Use Consul in Microservice

[consul configuration](https://docs.spring.io/spring-cloud-consul/docs/current/reference/html/#spring-cloud-consul-config)

### 1. Add dependency
- spring cloud is a separate project from string, so version has to be included

`pom.xml`
```xml
	<properties>
		<java.version>21</java.version>
		<spring-cloud.version>Hoxton.SR6</spring-cloud.version>
	</properties>

    		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-starter-consul-config</artifactId>
			<version>2.2.4.RELEASE</version>
		</dependency>

```
### 2. Add Configuration

Bootstrap Context
- in Spring Cloud applicaation there is a `Bootstrap Context`
- gets loaded before `Application Context`
- configuration data will be loaded during the bootstrap phase

Create `src/main/java/recources/bootstrap.yml`:
```yml
# server config
server:
  port: 9100

#application name config
spring:
  application:
    name: petMS    
# configuration for app to use consul config
  cloud:
    consul:
      config:
        # indicates that this microservice will use consul configuration
        enabled: true
        # default folder for configuration
        prefix: config
        # folder where common application properties are stored
        defaultContext: application
        # used to set the value of the separator used to separate profile names
        profileSeparator: '::'
        # format used
        format: YAML
```

Empty out `application.properties` file, as the values were moved from here to `bootstrap.yml`.


## Qustions
> Spring consul by deafault stores config data in ...?

In the file system.
## Error
[Error creating bean with name ConfigurationPropertiesBean](https://programmerah.com/solved-springboot-error-error-creating-bean-with-name-configurationpropertiesbeans-defined-in-class-path-48221/)

Problem is using springboot framework type, the introduction of the springcloud dependency, version incompatibility leads to errors can not find the bean