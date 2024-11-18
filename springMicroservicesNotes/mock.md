STEP 1

Basic Setup

Start Consul

Configure Service Discovery:

Configure gateway
in gateway `application.yml`
- server, port
- app name
-- cloud.consul.discovery.hostname

Configure MS
in ms `application.yml`
- server, port
- db username, password
- app name
- cloud.consul.dicovery hsotname


start both applications 
exectue tests
5 tests are passing
All tests pass for ConsulServerTest 3, and AadharDisoveryTest 2. (No central config needed)
Integration test did not pass (had type in uri which was the cause probably)

_____

ALTERNATIVE STEPS:
as long as the service class has @Service the controller can be built first and all controller tests will pass 

Adding @Transactional to Service did not help with test casesc
_____

STEP 2


AdharService
- @Service on top
- autowire validator
- autwire repo
- do isAadharVlaid
- DO NOT forget the check string equality with `.equals`

restart aadhar-ms
execute tests
- => 5 of 10 serviceTests are passing 
(total 10 tests)
_____________

STEP 3

COntroller
- @RestController
- @RequestMapping
>NEED @CrossOrigin
- autowire service IT HAS TO BE THE INTERFACE NOT THE IMPLEMENTATION
- add endpoint for valid aadhar 

Restart, execute got 2 of 4 controller tests
12 tests so far
both postmen test for this passes

________________
STEP 3

Add getAadharDetails in service 
check not found with `aadhar == null`

restart, execute
got 2 extra service points 7 of 10
toatal 14 tests


_______________
STEP 4

Add endpoint for get aadhar details in controller

restart, execute
got 1 extra controller test 3 of 4
total 16 as integration test works after tryign to fix application.yml in gatewaty (althouth it looks like did not change anything ???)
(but not the second time)

only 1 postmen passes for this 
3 of 6 total
( at the end all postman test pass)

___________
STEP 5

add service update address

restart, execute
got 1 extra service point 8 of 10
total 17

still the same 2 postmen tests pass

___________
STEP 6

add enpoint in controller for update address

restart, execute
got the last controller point 4 of 4
total 18

still only 2 postman test pass
_____________---


Added endpoint nonexistent aadhar passes n psotman but valid does not (it probably expects updated address that is not working yet)

no extra points

Added updateAddress service and endpoint get 1 extra service point
3of3 consul, 2of2 discovery 8of 10 service

postman
- all update address pass
- all valid pass
- 1 getdetails fail

the valid one
locahost:


RESTART




if controller has requetsmapping(value="/aadhar") the isvalid enpoint should have getmapping(value="")

sofar config for registration with consul that works and server porst that was 10 points only 1of3 consul and 1of1 discovery

no extra points when added:
gateway.discovery.locator.enabled: true

removed @Transactional from service class did not make any difference

PROBLEM found: misspelled aadhar-ms app name, gto 1 more consul point 2of3 now

ADDED routes and got the last of consul 3of3

NOW 13 

found adn corrected typo in route/uri made no difference sofar

added filters got the integration test point (first seemed to lost 4 points it may have gotten something restarting the servers just after executing tests)