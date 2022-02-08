createdAt: "2020-10-28T15:15:48.964Z"
updatedAt: "2020-10-28T15:38:35.886Z"
type: "MARKDOWN_NOTE"
folder: "7869a5810e7871ff4be9"
title: "JavaScript window"
tags: [
  "js"
  "javascript"
  "window"
  "tight_coupling"
  "name_collisions"
]
content: '''
  # JavaScript `window`
  
  [Window - Web APIs \\| MDN](https://developer.mozilla.org/en-US/docs/Web/API/Window)
  
  The `window ` object is provided by the browser environment and globally accessible to the JavaScript code using the identifier `window`.
  
  The `window` object is not part of the JavaScript specification, it's developed by [W3C](https:\\\\www.w3.org).
  
  The `window` object has access to a lot of information about the page itself. For example:
  - pages's URL: `window.location`
  - vertical scroll position of the page: `window.scrollY`
  - can scroll to a new position `window.scroll(x, y)`
  - can open a new page: `window.open(<URL>)`
  
  Every global variable declared with `var` (but **not** with `let` or `const`) is a property o. the `window` object. (But not those declared with `var` inside a function.)
  ```javascript
  var currentlyEating = 'ice cream';
  window.currentlyEating === currentlyEating;
  // True
  ```
  
  Any global function (not written inside another function)  is a method of the `window` object.
  
  ### Avoid using global variables due to:
  
  #### Tight Coupling
  In `tight coupling`, pieces of code are joined together in a way where changing one unintentionally alters the functioning of some other code.
  ```javascript
  var instructor = 'Richard';
  
  function richardSaysHi() {
    console.log(`${instructor} says 'hi!'`);
  }
  ```
  In the code above, the instructor variable is declared globally.
  The richardSaysHi() function does not have a local variable that it uses to store the instructor's name. Instead, it reaches out to the global variable and uses that. 
  If we refactored this code by changing the variable from instructor to teacher, this would break the richardSaysHi() function (or we'd have to update it there, too!).
  This is a (simple) example of tightly-coupled code.
  
  #### Name Collisions
  `Name collision` occurs when two (or more) functions depend on a variable with the same name.
  ```javascript
  let counter = 1;
  
  function addDivToHeader () {
    const newDiv = document.createElement('div');
    newDiv.textContent = 'div number ' + counter;
  
    counter = counter + 1;
  
    const headerSection = document.querySelector('header');
    headerSection.appendChild(newDiv)
  }
  
  function addDivToFooter() {
    const newDiv = document.createElement('div');
    newDiv.textContent = 'div number ' + counter;
  
    counter = counter + 1;
  
    const headerSection = document.querySelector('footer');
    headerSection.appendChild(newDiv)
  }
  ```
  Since both functions increment the counter variable, if the code alternates between calling addDivToHeader() and addDivToFooter(), then their respective divs will not have numerically ascending numbers. 
'''
linesHighlighted: []
isStarred: false
isTrashed: false
