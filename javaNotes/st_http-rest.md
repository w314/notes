
## HTTP

> What is HTTP? Why is it important to know about?

`HTTP` (`HyperText Transfer Protocol`) is a technique of transmitting data in a particular format, primarily between a server and a client.

HTTP works by a client making a connection to a `server`, sending a `request`, and receiving a `response`

The data tranmitted can be:

- `hypertext` - A text documents that have the special ability to link to one another.
- `hypermedia` - hypertext documents that have the ability to show multiple kinds of media

A `Request` contains:

- the `method` being used
- the `URL` where the target is
- version of HTTP is being used
- Optional information to help the server with the request (called `headers`)
- For some methods, a `body` which contains some resources (ex.: files to be uploaded)

A `Response` contains:

- version of HTTP is being used
- `status code` reflecting the outcome of the request
- `status message` which is shorthand and less descriptive than the status code
- Optional information to detail what happened with the request (called `headers` again)
- For some methods, a `body` which contains some resource (ex. file to be downloaded)

### HTTP verbs

> What are common HTTP verbs used when a client application is making a request?

- GET
  - used to retrieve data from a server at the specified resource
  - does not modify any resources
  - safe and `idempotent` method
- POST
  - used to send data to the API server to create or update a resource
  - the data sent to the server is stored in the request body of the HTTP request
  - `non-idempotent`
- PUT
  - similar to POST, PUT requests are used to send data to the API to update or create a resource
  - `idempotent`, calling the same PUT request multiple times will always produce the same result
  - when a PUT request creates a resource the server will respond with a 201 (Created), and if the request modifies existing resource the server will return a 200 (OK) or 204 (No Content)  TODO : no content???
- HEAD
- DELETE

  - deletes the resource at the specified URL

- PATCH

  - PATCH only applies partial modifications to the resource.
  - `non-idempotent`
  - with a PATCH request, you may only need to send the updated username in the request body - as opposed to POST and PUT which require the full user entity

- OPTIONS
  - an OPTIONS request should return data describing what other methods and operations the server supports at the given URL

### HTTP Status Codes

> What are some common HTTP status codes that can be included in a response?

HTTP Status Codes whether a specific HTTP request has been successfully completed.

Responses are grouped in five classes:

- Informational responses (100–199)
- Successful responses (200–299)
- Redirection messages (300–399)
- Client error responses (400–499)
- Server error responses (500–599)

Common Status Codes:

- 200 - OK, success
- 201 - Created
- 400 - Bad Request, client error
- 404 - Not Found
- 500 - Internal Server Error


## REST

An an architectural style for distributed hypermedia systems.

- Representational State Transfer (REST).
- has its guiding principles and constraints, these principles must be satisfied if a `service interface` needs to be referred to as `RESTful`
- `Web API` (or Web Service) conforming to the REST architectural style is a `REST API`

REST

- architecture for exposing information and functionality between software or devices
- information provided is a representation of the state of a given resource
- representation is usually JSON
- all communication uses HTTP

REST vs. SOAP vs. RPC

- REST vs. `SOAP` (`Simple Access Protocol`)
  - REST uses less bandwidth than SOAP
  - SOAP can only return xml, REST can return json, xml, yaml and more
- REST vs. `RPC` (`Remote Procedure Call`)
  - in REST users are not required to know procedure names or spedific parameters in a specific order

### REST Principles

- `Client-Server`

  - the client and the server should be separate from each other
  - client and server evolve independently

  <br>

  - `Uniform Interface`

  - key to the decoupling client from server is having a uniform interface
  - the following four constraints can achieve a uniform REST interface
    - Identification of resources – The interface must uniquely identify each resource involved in the interaction between the client and the server.
    - Manipulation of resources through representations – The resources should have uniform representations in the server response. API consumers should use these representations to modify the resources state in the server.
    - Self-descriptive messages – Each resource representation should carry enough information to describe how to process the message. It should also provide information of the additional actions that the client can perform on the resource.
    - Hypermedia as the engine of application state – The client should have only the initial URI of the application. The client application should dynamically drive all other resources and interactions with the use of hyperlinks.

  <br>

- `Stateless`

  - calls can be made independently of one another
  - each call contains all of the data necessary to complete itself successfully.

  <br>

- `Cachable`

  - a response should implicitly or explicitly label itself as cacheable or non-cacheable.

<br>

- `Layered System`
  - layered system style allows an architecture to be composed of hierarchical layers
  - in a layered system, each component cannot see beyond the immediate layer they are interacting with.

<br>

- `Code on Demand` (OPTIONAL)
  - allows for code or applets to be transmitted via the API for use within the application.

<br>

- `HATEOS` (**H**ypertext **A**s **T**he **E**ngine **O**f application **S**tate)
  - make API discoverable in state through links

### REST resources and URL construction

#### URI

`REST API`s use **U**niform **R**esource **I**dentifiers (`URI`s) to address resources.

The constraint of a `Uniform Interface` is partially addressed by the combination of URIs and HTTP verbs and using them in line with the standards and conventions.

#### REST Resource

- entity or data that API can provide info about
- can be identified by a URL
- can allow actions to be performed on it (GET, POST, PUT, DELETE)
- a resource can be a singleton or a collection.

##### Singleton and Collection Resources

- A resource can be a singleton or a collection.
- “customers” is a collection resource and “customer” is a singleton resource
  We can identify “customers” collection resource using the URI “/customers“. We can identify a single “customer” resource using the URI “/customers/{customerId}“.

##### resource archetypes categories:

- document
- collection
- store
- controller

###### document

A document resource is a `singular` concept that is akin to an object instance or database record.

In REST, you can view it as a single resource inside resource collection.

A document’s state representation typically includes both fields with values and links to other related resources.

Use “singular” name to denote document resource archetype.

Examples:

- `http://api.example.com/device-management/managed-devices/{device-id}`
- `http://api.example.com/user-management/users/{id}`
- `http://api.example.com/user-management/users/admin`

###### collection

A collection resource is a **server-managed directory of resources**.

Clients may propose new resources to be added to a collection. However, it is up to the collection resource to choose to create a new resource or not.

A collection resource chooses what it wants to contain and also decides the URIs of each contained resource.

Use the “plural” name to denote the collection resource archetype.

Examples

- `http://api.example.com/device-management/managed-devices`
- `http://api.example.com/user-management/users`
- `http://api.example.com/user-management/users/{id}/accounts`

Collection and Sub-collection Resources
A resource may contain sub-collection resources also.

For example, sub-collection resource “accounts” of a particular “customer” can be identified using the URN `“/customers/{customerId}/accounts”` (in a banking domain).

Similarly, a singleton resource “account” inside the sub-collection resource “accounts” can be identified as follows: “/customers/{customerId}/accounts/{accountId}“.

###### store

A store is a **client-managed resource repository**. A store resource lets an API client put resources in, get them back out, and decide when to delete them.

A store never generates new URIs. Instead, each stored resource has a URI. The URI was chosen by a client when the resource initially put it into the store.

Use “plural” name to denote store resource archetype.

Examples:

- `http://api.example.com/song-management/users/{id}/playlists`

###### controller

A controller resource models a **procedural concept**. Controller resources are like executable functions, with parameters and return values, inputs, and outputs.

Use “verb” to denote controller archetype.

Examples:

- `http://api.example.com/cart-management/users/{id}/cart/checkout`
- `http://api.example.com/song-management/users/{id}/playlist/play`

#### Best Practices

- use nouns for resources (users, posts, etc) not verbs
- use plurals for resources that are collections
- single resources are represented by a name or id
- send appropriate response code back

Forming URIs

- Put a resource into one archetype and then use its naming convention consistently.
- For uniformity’s sake, resist the temptation to design resources that are hybrids of more than one archetype.

Consistency is the key

Use consistent resource naming conventions and URI formatting for minimum ambiguity and maximum readability and maintainability. You may implement the below design hints to achieve consistency:

- use forward slash (/) to indicate hierarchical relationships between resources.

  - `http://api.example.com/device-management/managed-devices/{id}/scripts/{id}`

- Do not use trailing forward slash (/), it adds no semantic value and may confuse
- Use hyphens `-` to improve the readability of URIs, do not use underscores `_`

- use lowercase letters

- do not use file extensions

- use query component to filter URI collection, do not create new APIs – instead, enable sorting, filtering, and pagination capabilities in resource collection API and pass the input parameters as query parameters.
  - `http://api.example.com/device-management/managed-devices?region=USA&brand=XYZ&sort=installation-date`
