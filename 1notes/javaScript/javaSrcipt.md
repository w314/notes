javaScript, js

# JavaSrcipt

## About JavaScript
- dynamic, loosely typed
- used for WEB development (gives functionality to websites)

### JavaScript vs Java
### Objects
JavaScript
    
    - inheritance is through prototype mechanism in javaSript
    - 
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

## Template Literal

## Fetch API

## Async Await

## Promises





