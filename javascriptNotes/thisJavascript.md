createdAt: "2019-08-05T22:29:08.411Z"
updatedAt: "2020-10-29T20:21:05.676Z"
type: "MARKDOWN_NOTE"
folder: "7869a5810e7871ff4be9"
title: "JavaScript: this"
tags: [
  "JS"
  "this"
  "javascript"
]
content: '''
  # JavaScript: `this`
  Whenever  function is called a `this` variable is set to an object.
  
  The value of this inside a function depends on **how the function is invoked**.
  
  ## Invoking a constructor function
  Invoking a `costructor function` with the `new` operator sets `this` to the *newly-created object*.
  ```javascript
  function Cat(name) {
   this.name = name;
   this.sayName = function () {
     console.log(`Meow! My name is ${this.name}`);
   };
  }
  
  const bailey = new Cat('Bailey');
  ```
  
  ## Function invoked as a method
  
  ```javascript
  const dog  = {
    color : 'white',
    sayColor : function() {
      console.log(`I'm  a ${this.color} dog.`);
    },
  };
  
  dog.sayColor();
  ```
  > Outputs:
  I'm a white dog. 
  - `this` does not refer to the object it is defined
  - `this` is a method is not assigned to anything until an object calls the method
  - the value of `this` inside the `sayColor()` function is  whatever is left of the dot notation (whatever it was invoked on). In this case `this` will refer to the `dog` object it was invoked on.
  
  
  
  ## Function invoked as a regular function
  
  When a regular function is invoked the value of `this` is the global `window` object. 
  
  ```javascript
  function regularFunction() {
    this.myNewGlobalVariable = 'This refers to window.'
  }
  
  regularFunction();
  ```
  
  >It creates a new global variable `myNewGlobalVariable` which is a property of the `window` object.
  >
  More on [JavaScript window](:note:0c5ad18c-29ce-4fb5-9b0a-ad0789ba5a44).
  
  
  ## Setting the value of `this`
  ### `call()`
  `calls()` is a method directly invoked onto a function. (As Javascript function are *first class functions* they can have methods and properties)
  
  We first pass into it the value of `this`, than the receiving function's arguments.
  
  It makes it possible to *borrow* a method from one object and use it on another object.
  
  ```javascript
  const Andrew = {
    name: 'Andrew',
    introduce: function () {
      console.log(`Hi, my name is ${this.name}!`);
    }
  };
  
  const Richard = {
    name: 'Richard',
    introduce: function () {
      console.log(`Hello there! I'm ${this.name}.`);
    }
  };
  
  Richard.introduce.call(Andrew);
  // logging: Hello there! I'm Andrew.
  ```
  
  ### `apply()` vs. `call()`
  `apply()` works the same way as apply, just takes the parameters of the receving as an array
  ```javascript
  const dave = {
    name: 'Dave'
  };
  
  function sayHello(message) {
    console.log(`${message}, ${this.name}. You're looking well today.`);
  }
  
  // will set `this` to `window`
  sayHello('Bye');
  
  // both will set `this` to `cat`
  sayHello.call(dave, 'Nice to see you');
  sayHello.apply(dave, ['Hello']);
  ```
  ### bind()
  Problems with `this` when using **object methods as callback** function:
  ```javascript
  unction invokeTwice(cb) {
     cb();
     cb();
  }
  
  const dog = {
    age: 5,
    growOneYear: function () {
      this.age += 1;
    }
  };
  
  dog.growOneYear();
  // (this works as expected)
  
  dog.age;
  // 6
  
  invokeTwice(dog.growOneYear);
  // undefined
  
  dog.age;
  // 6
  ```
  *invokeTwice()* doesn't work as expected as it invokes *dog.grownOneYear* as a regular function not as a method of a the *dog* object. 
  As `this` in this case is set to `window`, the *age* property of the *dog* object doesn't change.
  
  There are two ways to solve this problem:
  - `anonymus clousre`
  ```javascript
  invokeTwice(function () { 
    dog.growOneYear(); 
  });
  
  dog.age;
  // 7
  ```
  `This` is still set to `window`, but this has no effect on the `closure` within the `anonymus function` and *grownOnYear* is called on the *dog* object.
  
  - `bind()` 
    - `Bind()` is method called on a function
    - allows us to define the value of `this`
    - **returns a new function** that, when called has `this` set to the value we give it
  ```javascript
  function invokeTwice(cb) {
     cb();
     cb();
  }
  
  const dog = {
    age: 5,
    growOneYear: function() {
      this.age += 1;
    }
  };
  
  invokeTwice(dog.growOneYear.bind(dog));
  console.log(dog.age); // 7
  ```
  
'''
linesHighlighted: [
  160
]
isStarred: false
isTrashed: false
