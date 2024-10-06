
# Monitoring

> Monitoring and measuring the usage of resources.


## `Actuator` Endpoints

- Spring provides several endpoints:
    - /actuator
    - /actuator/metrics
    - /actuator/health
- endpoints provide data for monitoring
    - threads
    - cache
    - requests
    - JVM memory
    - etc
- these details are provided with the `Micrometer` data provider


## `Micrometer`
> Converts metrics provided by Actuator to the format required by the Monitoring System.

- not part of the spring ecosystem
- open source project

### Why Micrometer?

Monitoring Systems like:
- Prometheus
- AWS Cloudwatch
- Netflix Atlas
- Grafana

Need metrics data in different format to process and display the output.


## `Prometheus`
> In memory dimensional time series database.

- operates on the `pull model`
- periodically pulls the metrics from the appliation
- has a simple buil-in ui
- to extract relevant metrics data
    - supports custom query language 
    - supports math operations

## Implement Monitoring with Prometheus


### 1. Install Prometheus
- download zip file
- extract files
- important files
    - `prometheus.exe` will start prometheus
    - `prometheus.yml` has the configuration to extract metrics and show them on the dashboard

### 2. Configure Prometheus

Open and modify `prometheus.yml`.
<br>Minimum configuration needed:

```yml
# global configuration
global:
  # set scrape interval to 15s, default is 60s
  scrape_interval: 15s
  # evaluate rules every 15s, default is 60s
  evaluation_interval: 15s
  # scrape_timeout is left to default 10s 
scrape_configs:
  # do it for each microservice
  # add name of microservice as job_name
  - job_name: 'CustomerMS'
    # set metrics path like below
    metrics_path: '/actuator/prometheus'
    static_configs:
      # set host and port for the microservice
      - targets:['localhost:9200']
```
- by default Prometheus pulls metrics from path `/metrics`
- to use path `/actuator/prometheus` we have to add dependecies in our spring boot project

### 3. Setup Microservice

#### 3.1 Add Dependency to Spring Boot Project

`pom.xml`
```xml
<dependecy>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-core</artifactId>
</dependency> 

<dependecy>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-registry-prometheus</artifactId>
</dependency> 
```

#### 3.2 Add properties to `application.properties` 

`application.properties`
```bash
# metrics endpoint over web is disabled by default, we enable it here
management.endpoint.metrics.enabled=true
# enable web exposure of all endpoints
# NOT needed to enable endpoint endpoint/actuator/prometheus
management.endpoints.web.exposure.include=*  
# enables  endpoint/actuator/prometheus endpoint
# this is where micrometer converts metrics to prometheus specified format
management.endpoint.prometheus.enabled=true
# enables the exporting of the metrics
management.metrics.export.prometheus.enabled=true
```

To enable the endpoint `endpoint/actuator/prometheus` the following config is needed
- management.endpoint.metrics.enabled=true
- management.endpoint.prometheus.enabled=true
- management.metrics.export.prometheus.enabled=true

#### 3.3 Restart Microservice

### 4 Start Prometheus

- Run `prometheus.exe`
- Prometheus runs on `localhost:9090`
- can check dashboard in a browser

To see raw data provided to prometheus formatted by micrometer (provided by actuator) about the microservice check `localhost:9200/actuator/prometheus`