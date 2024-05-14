
# Spring MVC (aka Spring Web)

Spring MVC is a module of the Spring Framework used to implement the Model-View-Controller architecture.

MVC Architecture
- Model - data related
- View - ui related
- Controller - business logic, interface between Model and View

## Spring MVC Structure

![Spring MV Structure](../image-2.png)


`DispatcherServlet`
- a Front Controller that which handles all the requests and responses (handles all HTTP traffic)

`HandlerMapping`
- an Interface that is responsible for sending requests to the proper controllers 
- tells the DispatcherServlet which controller takes which HTTP Request.  
- the most common implementation is the RequestMappingHandlerMapping which is what we’ll use (see @RequstMapping below)???????

`Controllers`
- are annotated with `@Controller` and are managed by DispacherServlet
    - stereotype annotation (makes a class a bean)
    - with more functionality in Spring MVC
    - in Spring MVC it indicates the class will handle HTTP requests
- `@RequestMapping`: This annotation in a `@Controller` Class specifies what URIs (endpoints) the controller will handle. It can be placed before the Class declaration or above a method declaration. 
- there are also `@___Mapping` (@GetMapping, @PostMapping) for methods within a Controller that specify what verbed requests go to that certain method
- the `ResponseEntity` object is used to send back responses to the client. It lets us set status code and the body of the response.  

`ContextLoaderListener` - This automates the creation of our ApplicationContext for us so that our application and its server can “just run”

## Spring MVC Application FLow
- When the `Tomcat server` receives a `HTTP request`, it gets passed to the `DispatcherServlet` (our Front Controller) 

- The `DispatcherServlet` consults the `HandlerMapping`(which looks for `@RequestMapping` annotations) to determine which controller to send the request to, based on the `URI` (the /endpoint) of the HTTP request. 

- The controller layer consults the service/business logic layer to process the request 

- (service, dao, and DB do their thing) 

- The controller builds the response, and hands it back to the DispatcherServlet 

- The DispatcherServlet then consults the ViewResolver if necessary to process a view (which we won’t use, since we will have our own frontend views) 

- The DispatcherServlet hands the response back to the Tomcat Server, which sends it to the front end (or wherever the request came from, like postman maybe) 

- The HTTP lifecycle starts again whenever a new request is sent! 
 
### Spring MVC Annotations
- `@RequestMapping`
    - is a class and method level annotation used to map web requests to spring controller methods
 ```java
 @RequestMapping(value ="/submit", method = RequestMethod.POST)
//  OR
@PostMapping("/users")
@GetMapping("/users")
@DeleteMapping("/users/{userId}")
// and so on
 ```

- `@PathVariable`
    - extracts values from the request URI **path**
    - not encoded
- `@RequestParam`
    - extract values form the request URI **query string**
    - encoded

## Sprign MVC Questions 
>What is it? 

Spring MVC is a module of the Spring Framework used to implement the Model-View-Controller architecture.

>What does MVC stand for?

MVC Architecture
- Model - data related
- View - ui related
- Controller - business logic, interface between Model and View

>What does it do for us?  

>What is its structure? What do the following classes/interfaces do: 
    > -  DispatcherServlet 
    >- HandlerMapping/RequestMappingHandlerMapping 
    >- ViewResolver 
    >- ContextLoaderListener 

>Know the SpringMVC application flow.  

>What is a Controller? 

>When are they Controllers called, and by what? 

>Know the annotations and what they do (annotations cheat sheet in the notes should be helpful) 

>Look into @RequestParam in the curriculum, just in case it’s asked 

>What is RestTemplate? What does it let us do? 
