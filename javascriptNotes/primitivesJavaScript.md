createdAt: "2019-08-14T19:30:25.792Z"
updatedAt: "2020-06-25T16:50:27.312Z"
type: "MARKDOWN_NOTE"
folder: "7869a5810e7871ff4be9"
title: "Primitives in JavaScript"
tags: [
  "JS"
  "javascript"
  "primitives"
]
content: '''
  # Primitives in JavaScript
  
  Primivite is data that is not an object and has no methods. There are 7 primitive data types:
  
  - string
  - number
  - bigint
  - boolean
  - null (the variable was given the value of nothing)
  - undefined (the varieable wasn't given any value)
  - symbol
  
  Primitives are immutable. If a variable is assigned a primitive it can be reassigned a new value, but the existing value cannot be changed as object properties can be altered.
  
  Using a string method doesn't mutate the string
  
  ```javascript
  let bar = 'foo';
  console.log(bar);
  \\\\ foo
  
  bar.toUpperCase();
  \\\\ FOO
  
  console.log(bar);
  \\\\ foo
  ```
  
  While using an array method mutates the array
  ```javascript
  let bar = [];
  
  console.log(bar);
  \\\\ []
  
  bar.push('foo');
  
  console.log(bar);
  \\\\ ['foo']
  ```
  
  An assignment gives a primitive a new (not a mutated) value. A primitive can be replace, but not directly altered.
  ```javascript
  bar = bar.toUpperCase();
  
  console.log(bar);
  \\\\ BAR
  ```
  
  When passing a primitive to a function it's passed as value, you are working a copy of it, the original is not affected.
  
  ```javascript
  let foo = 5;
  
  function addTwo(num) {
    num += 2;
  }
  
  \\\\ same function using the variable name as parameter
  function addTwo_v2(foo) {
    foo += 2;
  }
  
  addTwo(foo);
  console.log(foo);
  \\\\ 5
  
  addTwo_v2(foo);
  console.log(foo);
  \\\\ 5
  ```
  
  In the second function `addTow_v2` the `foo` variable is a second local `foo` variable. The external `foo` cannot be accessed due to lexical scoping and the resulting variable shadowing. (You'd have to use `window.foo` to access the external `foo` variable.)
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
