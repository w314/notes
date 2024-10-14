node, event

# Node.js Events

Node.js has built-in events:
    - `request event`
    - `response event`


Request & Response Events:
- internal events
- fire when a request is received by the server 
- or when a response is generated
- event listener implementation are available to handle these events

We can create custom events too.

## `EventEmitter Class`

Event handling is done by built-in EventEmitter class.

### Events of the EventEmitter Class

EventEmitter handles `POST`request with event:
- data event
    - fired when data flows in from POST request
- end event
    - fired when data fetching from client get completed 


### EventEmitter methods
- `on` 
    - used to bind and event with some functionality
- `end`
    - used to trigger and event


## Creating Custom Events

### 1. Create Custom Event

WITH MODERN JS SYNTAX
`VisitorCountModule.js` will count visitors to a website
```js
// custom event handler that counts the number users
// successfully logged in into the application

// load required modules
const EventEmitter = require('events').EventEmitter;
const util = require('util');

// number of visitors
let visitorCount;

// create VisitorCountClass
// extend EventEmitter class
class VisitorCountClass extends EventEmitter {

    // add constructor
    constructor(initialNo) {
        // first call super() - EventEmitter's constructor
        super();
        this.count = initialNo;
    }

    // add increment method
    increment() {
        this.count++;
        // emits a `visitor` event
        this.emit('visitor');
    }
}


// create object of our custom event class
const visitorCounter = new VisitorCountClass(0);

// with the on() method
// make our registerEventObject listen to the visitor event
// provide function to execute if visitor event happens
// provided function has to be proper function declaration, NOT arrow function
visitorCounter.on('visitor', function() {
    console.log(`The number of people visited: ${this.count}`);
    visitorCount = this.count;
})

// export a visitorCountEvent function
exports.visitorCountEvent = () => {
    // it will invoke the increment method of our registerEventObject
    visitorCounter.increment();
    // it will return the number of visitors
    return visitorCount;
}
```

WITH OLD JS SYNTAX

`VisitorCountModule.js` will count visitors to the website
```js
// custom event handler that counts the number users
// successfully logged in into the application

// load required modules
const EventEmitter = require('events').EventEmitter;
const util = require('util');

// number of visitors
let visitorCount;

// create constructor function
// has to be proper function declaration (NO arrow function)
const VisitorCountClass = function (initialNo) {
    this.count = initialNo;
}

// inherit constructor functon from EventEmitter class
util.inherits(VisitorCountClass, EventEmitter);

// extend prototype of constructor funtion 
// and add method that can emit the custom event 
VisitorCountClass.prototype.increment = function() {
    const self = this;
    // increases count
    self.count++;
    // emits a `visitor` event
    self.emit('visitor');
}

// create object of our custom event class
const visitorCounter = new VisitorCountClass(0);

// with the on() method
// make our registerEventObject listen to the visitor event
// provide function to execute if visitor event happens
// provided function has to be proper function declaration, NOT arrow function
visitorCounter.on('visitor', function() {
    console.log(`The number of people visited: ${this.count}`);
    visitorCount = this.count;
})

// export a visitorCountEvent function
exports.visitorCountEvent = () => {
    // it will invoke the increment method of our registerEventObject
    visitorCounter.increment();
    // it will return the number of visitors
    return visitorCount;
}
```

### 2. Use Even Handler in Server

`httpServer.js`
```js
// load required modules
const http = require('http');
// load custom event handler module
const visitorCounter = require('./VisitorCounterModule');

const server = http.createServer((req, res) => {
        // get visitor count
        // invokes eventModules visitorCountEvent
        const visitorCount = eventModule.visitorCountEvent();
        // write response
        res.writeHead(200, { ContentType: "text/html" });
        res.write(`<html>`);
        // stops browsers creating requests for favicon 
        // and therefore adding additional visitor counts
        res.write(`<head><link rel="icon" href="data:,"></head>`);
        res.write(`<body>`);
        res.write(`<p>The number of visitors whe visited the site: ${visitorCount}</p>`);
        res.write(`</body></html>`);
        res.end();
});

// start server
const port = 3001;
server.listen(port);
console.log(`Server is listening on port ${port}`);
```

### 3. The Process
1. server invokes visitorCounter module's visitorCount method
2. the visitorCount method invokes the increment method of our vistorCounter object
3. the increment method increases count and emits a `visitor event`
4. the visitorCounter object is set to listen to `visitor` events
5. in case of a `visitor` event our visitorCounter object will
    - console.log its count variable
    - set visitorCount variable to its own count variable
6. so after the visitorCountEvent method run the increment method of the visitorCounter object it will return the updated visitorCount


