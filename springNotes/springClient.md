WebClient, RestTemplate

# Making HTTP calls with Spring

Source: [Baeldung](https://www.baeldung.com/spring-webclient-resttemplate)

It’s a common requirement in web applications to make HTTP calls to other services. So, we need a web client tool.

There are two web client implementations in Spring:
- `RestTemplate`
- `WebClient`

## `RestTemplate` - blocking

- blocking
- uses the `Java Servlet API` under the hood
- based on a one thread per request model
- if lots of incoming requests wait for a slow thread:
    - threads will exhaust the thread pool
    - or will occupy the available memory
    - performance may degrade due to lots of thread switching
- see details in: springRetsTemplate.md

## `WebClient` - non blocking
- asynchronous, non-blocking solution
- provided by the `Spring Reactive Framework` 
    - uses event-driven architecture
    - `Reactive Streams API` provides means to compose asynchronous logic
    - can process more logic using fewer threads
- part of the `Spring WebFlux` library
- creates a "task" for each request
- puts those "tasks" in a queue
- will not block the executing thread while waiting for reponse to come back