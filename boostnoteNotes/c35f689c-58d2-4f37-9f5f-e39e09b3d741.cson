createdAt: "2020-11-04T17:19:39.578Z"
updatedAt: "2020-11-04T17:22:30.795Z"
type: "MARKDOWN_NOTE"
folder: "7869a5810e7871ff4be9"
title: "JavaScript Closure"
tags: []
content: '''
  # JavaScript Closure
  
  // from google javascript style guide:
  //   One thing to keep in mind, however, is that a closure keeps a pointer to its enclosing scope. As a 
  //   result, attaching a closure to a DOM element can create a circular reference and thus, a memory leak. 
  //   For example, in the following code: 
  
  ### Leaky example
  ```javascript
  function foo (element, a, b) {
    element.onclick = function() {
      // uses a and b
      // this func keeps a pointer to foo, 
      // and its enclosing scope
      // this func is attached to element, 
      // which thus keeps a pointer to foo
      // and its variables - a, b, element
    };
  }
  ``````
  
  - the function closure keeps a reference to element, a, and b even if it never uses element. Since element  also keeps a reference to the closure, we have a cycle that won't be cleaned up by garbage collection.
  
  ### In these situations, the code can be structured as follows:
  
  Solution example:
  ```javascript
  function foo (element, a, b) {
    element.onclick = bar(a, b);
  }
  
  function bar (a, b) {
    return function() {
      //uses a and b
    }
  }
  ```
'''
linesHighlighted: [
  7
  8
  24
]
isStarred: false
isTrashed: false
