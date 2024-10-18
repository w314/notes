node

# Node.js

> Node.js is a JavaScript runtime for building fast scalable network applications.

## Benefits
- full-stack JS development
- fast due to internal JS engine
- non blocking I/O model
- data streaming with built in `Sterams API`
- rich ecosystem managable with `NPM` package manager
- modular
- wide client-side and database connectivity
    - works with any client-side techonologies like Angular
    - and databases like MySQL or MongoDB


## Can be Used for

- SAP (Single Page Applications)
- real time application like chat rooms
- data streeming applications
- REST APIs
- server-side web applications

## Features

- V8 Engine
    - open source high performance engine for executing JavaScript
    - written in C++
    - compiles JS code to machine code
    - ultra fast gives Node.js applicaiton fast performance
    - developed by Google, also use in Google Chrome Browser
- Single Code Base
    - uses JavaScript
    - JS can manipulate JSON received from external web API resouces like MySQL or MongoDB
    - and that reduces processing time
- Asynchronous and Event Driven
    - Node.js server never waits for an API to return data to complete a request
    - will move to the next request to process
    - a notification mechanism is used to finish async processes
- Single-Threaded Event Loop Model
    - make Node.js highly scalable
    - based on JS's callback mechanism
- Scalability
    - Node.js uses Single Threaded Event Loop mechanism
    - it allows a Node app to serve a huge ammount of requests concurrently
    - as it automatically scales up to serve those requests
- I/O Bound Operations
    - as node is asynchronous/non-blocking
    - it can handle huge input-output operations
    - great for apps that have real-time data flowing in
- Streaming of data
    - Node has built-in Stream API
    - can stream data fast
- Modular
    - Node supports modular JS
    - helps with code maintenance and reusability   


## Where NOT to use Node.js

Node.js is NOT preferred for applications involving CPU-intensive operations.