 '''
  # JavaScript Closure
  

## Aware of memory leak
  From google javascript style guide:
  
 -t a closure keeps a pointer to its enclosing scope
 - as a result, attaching a closure to a DOM element can create a circular reference and thus, a memory leak. 
  
  For example, in the following code: 
  
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
  ```
  
  - the function closure keeps a reference to element, a, and b even if it never uses element
  
  - since element  also keeps a reference to the closure, we have a cycle that won't be cleaned up by garbage collection.
  
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
