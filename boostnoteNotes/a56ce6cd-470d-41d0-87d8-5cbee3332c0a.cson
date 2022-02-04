createdAt: "2019-08-14T15:56:36.909Z"
updatedAt: "2020-11-02T20:55:00.572Z"
type: "MARKDOWN_NOTE"
folder: "7869a5810e7871ff4be9"
title: "JavaScript Objects"
tags: [
  "JS"
  "javascript"
  "object"
  "iterable_protocol"
  "destructuring"
  "keys"
  "values"
]
content: '''
  # JavaScript Objects
  IN DOCS
  
  - An object is a data structure, an unordered collection of assicated key / value pairs.
  - Objects are passed by reference
  - [Object - JavaScript \\| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
  
  ## Creating an object
  
  - with `object-literal notation`
    - **recommended**, faster
    - the object constructor will be `Object()`
  
  ```javascript
  const dog = {
    name: 'Pöttöm',
    age: 1,
    friends: {
      name: 'Lexi',
      type: 'dog'
    }
  }
  ```
  
  - with `constructor function`
  ```javascript
  const myDog = new Dog();
  ```
  #### about constructor functions
  What makes a function a `constructor function`?
    - invoking it with `new` keyword
    - the way it's coded internally
      - uses `this`
      - doesn't return anything
      
    ```javascript
    function Dog(name) {
      this.age = 2;
      this.name = name;
    }
    ```
  This function will add the *age* property with value *2* to any new object it creates and gives them the *name* it received as a parameter.
  Using the `new` keyword makes `this` refer to the new object being created. If invoked without the `new` keyword, it will return `undefined` as it has no return statement.
  (As convention constructor function names start with capital letter.)
  
  #### instanceof operator
  The `instanceof` operator checks if the constructor appears in the object's `prototype chain`.
  
  ```javascript
  myDog instaceof Dog;
  // returns true
  ```
  
  ### Object literal shorthand
  
  instead of:
  
  ```javascript
  let type = 'quartz';
  let carat = 21.19;
  
  const gemstone = {
    type: type,
    carat: carat,
    
    calculateWorth = function() {
      // calculates worth
    }
  };
  ```
  
  in `ES6`:
  ```javascript
  let type = 'quartz';
  let carat = 21.19;
  
  const gemstone = {
    type,
    carat,
    calculateWorth() {...}
  };
  
  ```
  
  ## Accessing Object Properties
  - `dot notation`
  ```javascript
  dog.color;
  ```
  Limitations of the dot notation:
  ```javascript
  // When the key is a number
  const number = { 1: 'one'};
  number.1;  // Uncaught SyntaxError: Unexpected number
  number[1];  // one
  
  // When variables are assigned to property names
  const dog = {color: 'white'};
  const myVariable = 'color';
  dog[myVariable];  // white
  // the variable myVariable gets substituted with the value of myVariable ('color') and dog['color'] is 'white'
  dog.myVariable;  // undefined
  // as all keys are strings and there is no key 'myVariable'
  ```
  
  
  - `square bracket notation`
  ```javascript
  dog['color'];
  ```
  
  #### accessing nested objects:
  ```javascript
  dog.friend.name;
  dog['friend']['name'];
  ```
  
  
  ### Modifying object properties
  - data within objects are mutable
  
  ```javascript
  dog.age += 1;
  ```
  
  ### Adding object properties
  
  ```javascript
  dog['favourite food'] = 'meat';
  
  dog.greet = function() {
   console.log(`Hi, my name is ${this.name}!`);
  };
  ```
  
  ### Removing object properties
  
  ```javascript
  delete dog['name'];
  
  dog['name'];
  // undefined
  ```
  
  ## Object Methods
  - methods are properties that point to functions
  - methods can access the properties of the object they were called on with the `this` keyword
  
  ```javascript
  let umbrella = {
    color: 'pink',
    isOpen: true,
    
    open: function() {
      if(this.isOpen){
          return `This ${this.color} umbrella is already open`;
      } else {
        this.isOpen = true;
        return 'opened umbrella' ; 
      }
    }
  };
  
  // invoking the method
  umbrella.open();
  umbrella['open']();
  ```
  
  ## `Destructuring` values from object
  ```javascript
  const gesmstone = {
    type: 'quartz',
    carat: 21.29
  } 
  
  const {type, carat} = gemstone
  // this also works:
  const {carat} = gemstone
  ```
  
  ## Extracting `keys` and `values`
  
  The `Object()` functions includes these two methods:
  - [Object.keys() - JavaScript \\| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys)
  - [Object.values() - JavaScript \\| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/values)
  Object.values() support has to be checked for the browser used.
  
  ```javascript
  const myWords = {
    car: 'automobile',
    apple: 'healthy snack',
    cat: 'cute',
    dog: 'friend'
  };
  
  Object.keys(myWords);
  // ['car', 'apple', 'cat', 'dog']
  Object.values(myWords);
  // ['automobile', 'healthy snack', 'cute', 'friend']
  ```
  
  ## Objects are passed as reference
  
  - In JavaScript a primitive (string, number, bigint, boolean, null, undefined, symbol) is immutable, when passed to a function, but objects are passed as reference and are mutable.
  - Same things happen when you copy them to an other variable
  ```javascript
  const iceCreamOriginal = {
    Andrew: 3,
    Richard: 15
  };
  
  const iceCreamCopy = iceCreamOriginal;
  
  iceCreamCopy.Richard = 99;
  
  iceCreamCopy.Richard;  // 99
  
  iceCreamOriginal.Richard;  // 99
  ```
  
  
  ## `Iterable Protocol`
  - Allows JavaScript objects to define and customize their **iteration behavior**.
  
  - `for ... of loop` iterates over `iterable objects`, objects that have implemented the itarable interface
  
  
  ## Prototype
  [Inheritance and the prototype chain - JavaScript \\| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)
  [Object prototypes - Learn web development \\| MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_prototypes)
  
  - All functions **with the exceptions of arrow functions** have a  `prototype property` in JavaScript. This prototype property is an object. *(DO NOT USE ARROW FUNCTIONS WHEN CREATING PROTOTYPE METHODS)*
  - All object created by the constructor function keep a reference to the prototype. When created, a property named `__proto__` is added to them, which points to the objects prototype. 
  **DO NOT reassign the `__proto__` property or use it in your code. Do not use it to manage inheritance.**
  [Object.prototype.__proto__ - JavaScript \\| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/proto)
  
  When adding methods to the constructor function, all objects created will have this method created in them as one of their methods. Should you want to change this method, you'd have to change it in all of the objects. To save memory and not repeating ourselves `DRY` (Don't Repeat Yourself), we can add method's to the constructor object's prototype property.
  
  - As all objects created by the constructor functions has a link to the constructor's prototype they can use access the prototype's methods as their own.
  - The prototype property is an object, which also has links to its own prototype property creating a `prototype chain`.
  - Javascript leverages the link between object and its prototype to implement `inheritance`.
  - When invoking a method on an object or accessing a property of it the JavaScript interpreter looks for them first within the object's own methods and properties, then in it's prototype and then further along the `prototype chain`.
  - Similar for variable `shadowing` methods defined directly in teh object takes precedence over any properties or methods defined further up in the prototype chain.
  - At the very end of the `prototype chain` is the `Object()` object.
  
  #### replacing the prototype object
  
  - You can add methods to the prototype later, and object created before adding the new method can still use it.
  - If you replace the prototype objects created before the prototype replacment will work according to the old prototype, objects created after according to the new one.
  ```javascript
  function Hamster() {
    this.hasFur = true;
  }
  
  let waffle = new Hamster();
  
  // add a method later
  Hamster.prototype.eat = function () {
    console.log('Chomp chomp chomp!');
  };
  
  // object created before can use it
  waffle.eat();
  // 'Chomp chomp chomp!'
  
  
  // REPLACE PROTOTYPE
  Hamster.prototype = {
    isHungry: false,
    color: 'brown'
  };
  
  // previously created object will still follow old prototype
  console.log(waffle.color);
  // undefined
  waffle.eat();
  // 'Chomp chomp chomp!'
  
  // newly created object the new one
  const muffin = new Hamster();
  muffin.eat();
  // TypeError: muffin.eat is not a function
  console.log(muffin.isHungry);
  // false
  ```
  
  ## Checking an Object's Properties
  
  ### hasOwnPorperty()
  [Object.prototype.hasOwnProperty() - JavaScript \\| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)
  Returns true if the property belongs to the object itself and is not inherited. Properties defined in the object itself are owned, while those in the object's prototype are inherited.
  ```javascript
  function Phone() {
    this.operatingSystem = 'Android';
  }
  
  Phone.prototype.screenSize = 6;
  
  const myPhone = new Phone();
  myPhone.hasOwnProperty('operatingSystem');  // true
  myPhone.hasOwnProperty('screenSize');  // false
  ```
  
  ### isPrototypeOf() and getPrototypeOf()
  
  [Object.prototype.isPrototypeOf() - JavaScript \\| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/isPrototypeOf)
  [Object.getPrototypeOf() - JavaScript \\| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/getPrototypeOf)
  Are ways to check if an object exists in another object's `prototype chain`.
  ```javascript
  // rodent object
  const rodent = {
    favoriteFood: 'cheese',
    hasTail: true
  };
  
  // Mouse() constructor function
  function Mouse() {
    this.favoriteFood = 'cheese';
  }
  
  // assign Mouse() prototype to rodent object
  Mouse.prototype = rodent;
  
  // create a new Mouse object
  const ralph = new Mouse();
  
  rodent.isPrototypeOf(ralph);  // true
  const myPrototype = Object.getPrototypeOf(ralph);
  
  console.log(myPrototype);
  // { favoriteFood: 'cheese', hasTail: true }
  ```
  
  ### constructor property
  [Object.prototype.constructor - JavaScript \\| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/constructor)
  Each time an object is created, a special property is assigned to it under the hood: `constructor`.
  Accessing the object's `constructor property` returns a reference to the `constructor function` that created the object.
  ```javascript
  function Longboard() {
    this.material = 'bamboo';
  }
  
  const board = new Longboard();
  
  console.log(board.constructor);
  // function Longboard() {
  //   this.material = 'bamboo';
  // }
  ```
  
  If the object was created using `literal notation` it's constructor is the built in `Object()` function.
  
  ## Inheritance - Object.create()
  [Object.create() - JavaScript \\| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create)
  
  - Inheritance in JavaScript is about setting up the prototype chain.
  - `Object.create()` takes in a parent object and returns a new object with its '__proto__' property set to that parent object.
  - JavaScript objects can only be prototype-linked to a single object (`single inheritance`).
  ```javascript
  const person = {
    isHuman: false,
    printIntroduction: function() {
      console.log(`My name is ${this.name}. Am I human? ${this.isHuman}`);
    }
  };
  
  const me = Object.create(person);
  
  me.name = 'Matthew'; // "name" is a property set on "me", but not on "person"
  me.isHuman = true; // inherited properties can be overwritten
  
  me.printIntroduction();
  // expected output: "My name is Matthew. Am I human? true"
  
  ```
  
  ## Mixins - Object.assign()
  [Object.assign() - JavaScript \\| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
  
  - A `mixin` is a technique that takes the properties and methods from one object and copies them over to another object.
  - `Object.assign(<target>, <source>)` doesn't return a new object. It directly modifies and returns the target object it was passed in. 
    - properties from the source object are copied over
    - values of existing properties of target object with same name in source object will be overwritten
    - properties of target object, that doesn't exist in source object will remain intact
  ```javascript
  let target = { letter: 'a', number: 11 };
  
  let source = { number: 7 , color: 'purple'};
  
  Object.assign(target, source);
  
  console.log(target);
  // { letter: 'a', number: 7, color: 'purple' }
  ```
  #### mixin multiple source objects
  - Order of source object matter, properties with the same name in object later in the list will overwrite the value given to the property before.
  - **Doesn't modify prototype chains**. The created object is not in the `protoype-chain` of the source object and vice versa. In this example *platypus's* constructor is *Object()*.
  - Was introduces in ES6, browser compatibility may be an issue.
  ```javascript
  const duck = {
    hasBill: true,
    feet: 'orange'
  };
  const beaver = {
    hasTail: true
  };
  const otter = {
    hasFur: true,
    feet: 'webbed'
  };
  
  const platypus = Object.assign({}, duck, beaver, otter);
  
  console.log(platypus);
  // {hasBill: true, feet: 'webbed', hasTail: true, hasFur: true}
  ```
  
  ## Factory Functions
  A `factory function` is a function that returns an object, but isn't itself a calss or constructor.
  ```javascript
  function Radio(mode) {
    let on = false;
  
    return {
      mode: mode,
      turnOn: function () {
        on = true;
      },
      isOn: function () {
        return on;
      }
    };
  }
  
  // creat a new object
  let fmRadio = Radio('fm');
  
  // fmRadio closes over the Radio's on varible
  // even though it cannot be accessed externally
  fmRadio.on;  //undefined
  fmRadio.isOn();  // false
  fmRadio.turnOn();  
  fmRadio.isOn(); // true
  ```
  
  They can be used to combine object when creating a new object
  ```javascript
  function IceCreamFactory(obj) {
    let isCold = true;
  
    return Object.assign({}, obj, {
      melt: function () {
        isCold = false;
      },
      isCold: function () {
        return isCold;
      }
    });
  }
  
  let iceCream = IceCreamFactory({});
  
  
  function ConeFactory(obj) {
    let isDry = true;
  
    return Object.assign({}, obj, {
      soggy: function () {
        isDry = false;
      },
      isDry: function () {
        return isDry;
      }
    });
  }
  
  let iceCreamCone = IceCreamFactory(ConeFactory({}));
  
  console.log(iceCreamCone);
  // {soggy: f, isDry: f, melt: f, isCold: f}
  ```
  
  ## Private Properties
  
  >**Javascript has no concept of private properties out-of-the-box**.
  >
  
  `Closures` provide a way to create private data.
  
  ```javascript
  function myCounter() {
    let count = 0;
  
    return function () {
      count += 1;
      return count;
    };
  }
  
  let counter = myCounter();
  // out counter object uses myCounter's count variable to count
  counter();  // 1
  counter(); // 2
  
  // and this count variable is unaccessible externally
  counter.count;  // undefined
  count; // undefined
  ```
  
  ### Module Pattern
  - At its core, the Module Pattern leverages scope, closures, and (commonly) IIFE's to not only hide data from external access, but to also provide a public interface for such data.
  - Module Pattern is used when you just want one "version" of an object. If you're looking to instantiate unique objects that follow a certain blueprint, you can always still write and invoke a constructor function!
  ```javascript
  // lets create an IIFE
  let person = (function () {
    let name = 'Veronika';
  
    return  {
      getName: function () {
        return name;
      },
      setName: function (myName){
        name = myName;
      }
    };
  })();
  
  // the name variable is hidden
  person.name;  // undefined
  
  // we can acces and modify the variable through methods
  person.getName;  // 'Veronika'
  person.setName('Not Veronika');
  person.getName;  // 'Not Veronika'
  ```
  
  ### Revealing Module Pattern
  `Revealing Module Pattern` is a slight variation of `Module Pattern`. It involves:
  - an `IIFE`
  - local variables and methods
  - a returned object literal with keys that point to data intended to be revealed
  
  ```Javascript
  // create object person with Revealing Module Pattern 
  let person = (function () {
    let privateAge = 0;
    let privateName = 'Andrew';
  
    function privateAgeOneYear() {
      privateAge += 1;
      console.log(`One year has passed! Current age is ${privateAge}`);
    }
  
    function displayName() {
      console.log(`Name: ${privateName}`);
    }
  
    function ageOneYear() {
      privateAgeOneYear();
    }
  
    return {
      name: displayName,
      age: ageOneYear
    };
  })();
  
  
  // using name() method we can use the private displayName() function
  console.log(person.name()); // 'My name is Andrew'
  
  // as displayName() is not a 'property' of person you cannot use it directly
  console.log(person.displayName());  // undefined
  
  
  // using the name method uses the private 'privateName' property
  console.log(person.name());  // 'My name is Andrew'
  
  // if you do this:
  person.privateName = 'Richard';
  console.log(person.privateName); // 'Richard'
  console.log(person.name());  // 'My name is Andrew'
  /*
  you have added a `privateName` property to 'person', 
  but the `name()` method will always use 
  the `privateName` property inside the `IIFE`
  */
  ```
'''
linesHighlighted: [
  510
  484
  395
  22
]
isStarred: false
isTrashed: false
