createdAt: "2020-06-25T17:24:06.976Z"
updatedAt: "2020-06-30T20:21:41.443Z"
type: "MARKDOWN_NOTE"
folder: "7869a5810e7871ff4be9"
title: "Javascript Loops"
tags: [
  "js"
  "javascript"
  "loops"
  "while"
  "for"
  "for_in"
]
content: '''
  # Javascript Loops
  
  ## while loop
  ```javascript
  let start = 0
  
  while (start < 5) {
    console.log(start);
    start += 2;
  }
  
  // 0 2 4 
  ```
  
  ## For Loops
  
  ### For Loop (regular)
  - Loops over data that is iterable.
  - Objects are not included as they are not iterable by default.
  
  ```javascript
  const digits = [0, 1, 2, 3]
  
  for (let i = 0; i  digits.length; i++) {
    console.log(digits[i]);
  }
  
  // 0 1 2 3
  ```
  
  ### For Of Loop
  
  - Works with objects
  - You can stop or break it any time
  - Only loops over values of the object, won't loop over properties like for in loop
  
  ```javascript
  const digits = [0, 1, 2, 3]
  
  for (const digit of digits) {
    console.log(digit);
  }
  
  // 0 1 2 3
  ```
  
  
  ### For In Loop
  
  - Loops over data that is iterable.
  - Objects are not included as they are not iterable by default.
  - **Do not use when looping over arrays** as it loops over all enumerable properties. If you add any additional properties to the array's prototype:
  
  ```javascript
  Array.prototype.decimalfy = function() {
    for(let i = 0; i < this.length; i++) {
      this[i] = this[i].toFixed(2);
    }
  };
  
  const digits = [0, 1, 2]
  
  for (const index in digits) {
    console.log(digits[index]);
  }
  
  /* WILL PRINT:
   0
   1
   2
   function() {
     for (let i = 0; i < this.length; i++) {
        this[i] = this[i].toFixed(2);
      }
    }
  */
  
  ```
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
