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

## Arrays

## Functions
- arrow functions

## closures

## this 

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

## Fetch API

## Async Await

## Promises





