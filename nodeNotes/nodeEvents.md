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

### Syntax

```js
// load EventEmitter and util modules
const EventEmitter = require('events').EventEmitter;
const util = require('util')

// create constructor function
const className = function() {};

// inherit constructor function from EventEmitter class
util.inherits(className, EventEmitter);

// extend prototype of the constructor function
// add method that can emit the custom event
className.prototype.methodName = () => {
    classobject.emit(eventName);
};

// listen for event
// perform approriate action using on method
classObject.on(eventName, () => {});
```


Event to count visitors on a website:
```js
// load EventEmitter and util modules
const EventEmitter = require('events').EventEmitter;
const util = require('util')

// RegisterEventClass is create using constructor function
// will count visitors visiting our site
const RegisterEventClass = (initialNo) => {
    this.count = initialNo;
}

// inherit constructor function from EventEmitter class
util.inherits(RegisterEventClass, EventEmitter);

// extend prototype of constructor function
// and add an increment method to it
// increment method will emit an event name visitor
RegisterEventClass.prototype.increment = () => {
    const self = this;
    self.count++;
    // name event that will be emitted
    self.emit('visitor');
}

// create new RegisterEventeClass object
const access = new RegisterEventClass(0);


// set behavior on object in case of `visitor` event
acces.on('visitor', () => {
    console.log(`The number of people visited:: ${this.count}`);
    globalcount = this.count;
})

exports.visitorCountEvent = () => {
    access.increment();
    return globalCount;
}
```
