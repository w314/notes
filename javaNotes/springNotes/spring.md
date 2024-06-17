review:
https://hellokoding.com/jpa-hibernate-composite-primary-key-entity-mapping-example-with-mysql/

Why use Spring in project?

developer can focus on logic not configuration
dependency injection

- it is a lightweigth application framework


Spring replaced EJB (Enterprises Java Bean)

without sublet container you could nto use spring container

Why are you using tomcat

tomcat is a webserver = server that will manage web container


spring container is inside servlet container
tomcat container 

security you will implemetn at teh container level not the bean level

what is lightweight


third party services you inject into container, all the beans inside can use that service


spring container does not have inbuilt services inside therefore it is lightweigt.

If you need services you can inject them.

____________________________

If i change the nam eof the controller 

how does @ComponentScan

if I change com.wp.contorller to com.controller will Spring recongize the controller class?

@ComponentScan is already included with @SpringBootApplication annotation.
it will scan groupid.artifactid (com.wp.controller)

what if you want to scan some user defined pacakges
if you want different packages you have to overwrite the default ComponentScan with
@ComponentScan(basePackages = {"com.*})

Difference between web application and web services?
web service not dependent on language
web app is langugage dpeendent


web services uses mediator that create an API from service


aservices are API-s , response goes to client =in JSON format. JSON response is created by jackson JSON
Jackson library converts response to JSON

default response of controller is 
