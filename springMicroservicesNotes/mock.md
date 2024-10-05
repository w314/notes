Configure Service Discovery:

in gateway ```application.yml`
- server, port
- app name
-- cloud.consul.discovery.hostname

in ms
- server, port
- db username, password
- app name
- cloud.consul.dicovery hsotname


All tests pass for ConsulServerTest 3, and AadharDisoveryTest 2. (No central config needed)

_____

AdharService
- @Service on top
- autowire validator
- autwire repo
- do isAadharVlaid
- => 5 serviceTests are passing (total 10 tests)



COntroller
- @RestController
- @RequestMapping
- autowire service 
- added handle for isvalid lost two tests
- added @CrossOrigin got the 2 tests back.
>NEED @CrossOrigin


NO extra points so far, although both postman test for isValid endpoint pass

Added getAadharDetails in service got 2 service points - 12


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