javaScript, js

# JavaSrcipt

## About JavaScript
- dynamic, loosely typed
- used for WEB development (gives functionality to websites)

### JavaScript vs Java
- Compiled / Interpreted
  - JS is interpreted
  - Java is compiled
- Varibales
  - JS is loosely typed
  - Java is strongly typed
-  Objects    
    - in JS inheritance is through prototype mechanism
    - in Java through classes
- Threads
  - JavaScript is single threaded
  - Java is multithreaded
    - 
## Variables

Available variable declarations
JavaScript has three kinds of variable declarations.

`var` - Declares a variable, optionally initializing it to a value.

`let`- Declares a block-scoped, local variable, optionally initializing it to a value.

`const` - Declares a block-scoped, read-only named constant.

## Data Types

- let
- const
## Scope

## Variables

## Objects


### `Object.freeze()
> Method used to make object immutable.
Object.freeze is `shallow`, it only affects the immediate properties of th object. 

If the objects contains other objects (like arrays or other JS object) those can still be modified.

```js
const obj = {
    prop: 42
};

Object.freeze(obj);

obj.prop = 33; // This will not have any effect
console.log(obj.prop); // Outputs: 42
```

- use `Object.isFrozen() to check if an object is frozen.

## Arrays

## Functions

- arrow functions
### Callback & Higher Order Funtions
A `higher order funtion` is a function that takes an other function as an argument.

The function passed as the argument is a `callback funtion`.


## closures

## this 
>In JavaScript, when we used in a funtion, the this keyword directs to an object to which it is bound.

Types of binding in JavaScript
- Default binding
  - outside of function: global object
  - inside function: 
    - strict mode: undefined
    - non-strict mode: global object
  - event handlers: object that received the event

- Implicit binding
- Constructor call binding
- Explicit binding
## Type coersion

## DOM (Database Object Model)


### JavaScript DOM Manipulations
  
#### Add Element
  
  To avoid extra `reflows` create fragment, add elements to fragment before adding fragment to page.
  ```javascript
  const fragment = document.createDocumentFragment();  // ← uses a DocumentFragment instead of a <div>
  
  for (let i = 0; i < 200; i++) {
      const newElement = document.createElement('p');
      newElement.innerText = 'This is paragraph number ' + i;
  
      fragment.appendChild(newElement);
  }
  
  document.body.appendChild(fragment); 
  // reflow and repaint here -- once!
  ```
  
  #### Add Attributes to Elements
  ```javascript
  const element = document.createElement('p');
  element.setAttribute('id', 'elementId');
  ```
  
  #### Add Class to Element
  ```javascript
  const div = document.createElement('div');
  div.className = 'foo';
  
  // use the classList API to remove and add classes
  div.classList.remove("foo");
  div.classList.add("anotherclass");
  

  // toggle class
  //  if class visible is part of the classList remove it, otherwise add it
  div.classList.toggle("visible");
  
  // toggle visible, depending on a conditional
  div.classList.toggle("visible", i < 10 );
  
  // check if a class is in classList
  console.log(div.classList.contains("foo"));
  
  // add or remove multiple classes
  div.classList.add("foo", "bar", "baz");
  div.classList.remove("foo", "bar", "baz");
  
  // add or remove multiple classes using spread syntax
  const classes = ["foo", "bar"];
  div.classList.add(...classes);
  div.classList.remove(...classes);
  
  // replace class "foo" with class "bar"
  div.classList.replace("foo", "bar");
  ```


## Event Listeners

### Event
> Events are things that happen in the system you are programming.
- the system produces (or "fires") a signal of some kind when an event occurs
- and provides a mechanism by which an action can be automatically taken (that is, some code running) when the event occurs
- examples:
  - user clicks a button
  - browser loads page

### Event Capturing

The standard DOM Events describes 3 phases of event propagation:

- `Capturing phase` – the event goes down to the element.
- `Target phase` – the event reached the target element.
- `Bubbling phase` – the event bubbles up from the element.

To catch an event on the capturing phase, we need to set the handler capture option to true:
```js
elem.addEventListener(..., {capture: true})
```




### How to handle events
#### `addEventListener()`
Objects that can fire events have an `addEventListener()` method.

#### To add event listener:
```js
// select element
const btn = document.querySelector("button");

// add event listener
btn.addEventListener("click", () => {
  console.log("I was clicked!")
});

// ************* OR *************

// create named function
function sayClicked() {
 console.log("I was clicked!")
}

// use function name in addEventListener
btn.addEventListener("click", sayClicked);
```
Add multiple event listeners:
<br>By making more than one call to addEventListener(), providing different handlers, you can have multiple handlers for a single event
```js
myElement.addEventListener("click", functionA);
myElement.addEventListener("click", functionB);
```

Use the `event handler property`
```js
// CANNOT ADD MULTIPLE LISTENER THIS WAY
// SECOND WOULD OVERWRITE THE FIRST
btn.onlcick = () => {console.log("I am clicked!")}
// or
btn.onclick = sayClicked;
```


#### To remove event listener
```js
btn.removeEventListener("click", sayClicked);
```


### Event Object
- automatically passed to event handlers
- the `target` property of the event object is a reference of the object the event accured upon
- can have extra properties (eg: keydown event object has a key property)

### Preventing default behavior
THe `eventObject.preventDefault()` method of the event object will prevent default behavior for example submitting a form when the submit button is clicked.

### Event Bubbling


## Template Literal
Template literals are literals delimited with backtick (`)  characters, allowing for multi-line strings and  string interpolation with embedded expressions.

```js
const name = "Bobek";
console.log(`Hi ${name}!`);
```

## Promises
A Promise is a proxy for a value not necessarily known when the promise is created. It allows you to associate handlers with an asynchronous action's eventual success value or failure reason.

- Promise is an object 
- it represents the eventual completion (or failure) of an asynchronous operation and its resulting value

A Promise is in one of these states:

- `pending`: default initial state, neither fulfilled nor rejected.
- `fulfilled`: meaning that the operation was completed successfully.
- `rejected`: meaning that the operation failed.

The eventual state of a pending promise either:
- `fulfilled` with a value 
- `rejected` with a reason (error)

When either of these options occur, the associated handlers  are called. 


### How to create a Promise
- create a new Promise intance <br>
`const myPromise = new Promise()`
- the constructor takes one argument a (callback) function <br>
`const myPromise = new Promise(() => {})`
- the callback functions is passed two arguments
<br>`const myPromise = new Promise((resolve, reject) => {})`
  - `resolve`: a function that allows you to change the status of the promise to `fulfilled`
  - `reject`: a function that allows to change the status fo the promise to `rejected`

```js
const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve(); // Change status to 'fulfilled'
  }, 2000);
});
```
### How to listen to Promises
- When you create a new Promise, you're really just creating a plain old JavaScript object. 
  - This object can invoke two methods, then, and catch. - when the status of the promise changes to fulfilled, the function that was passed to .then will get invoked - when the status of a promise changes to rejected, the function that was passed to .catch will be invoked.
```js
function onSuccess() {
  console.log("Success!");
}

function onError() {
  console.log("💩");
}

const promise = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve();
  }, 2000);
});

promise.then(onSuccess);
promise.catch(onError);
```

## Async Await
- returns a Promise
- the `await` keyword makes js wait untill the promise is settled


## Fetch API
>The Fetch API interface allows web browser to make HTTP requests to web servers.
- promise based
- asynchronous
- takes to arguments:
  - url
  - init object you can use to set for example:
    - `method: POST`
    - `headers: {}`
    - `body:`
```js
async function logMovies() {
  const response = await fetch("http://example.com/movies.json");
  const movies = await response.json();
  console.log(movies);
}
```






