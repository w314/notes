
  # JavaScript Array
  ```javascript
  myArray = [1, 2, 'szia'];
  
  console.log(myArray.length);
  //3
  
  // Get last element:
  myArray[myArray.length-1];
```

## Max of Array
```javascript
const nums = [3, 7, 2]
const maxValue = Math.max.(...nums)
  ```
  
  ## Array Properties
  - length
  
  ## Array Methods
  - sort()
  - reverse()
  - push()
  - `pop()` - removes and returns the last element of the array, returnes `undefined` when array is epmty
  - `shift()` removes and returns first element of array
  - `unshift()` adds new element to the beginning of the array and returns new array length
  - concat()
  - `splice()` 
    - changes the contents of the array
    - can be used for insertion or deletion
    - returns deleted elements
  ```javascript
  // REMOVE 0 ELEMENTS AND INSERT TWO AT INDEX 2
  
  let myFish = ['angel', 'clown', 'mandarin', 'sturgeon']
  let removed = myFish.splice(2, 0, 'drum', 'guitar')
  
  // myFish is ["angel", "clown", "drum", "guitar", "mandarin", "sturgeon"] 
  // removed is [], no elements removed
  
  // REMOVE ELEMENT AT INDEX 3
  let myFish = ['angel', 'clown', 'drum', 'mandarin', 'sturgeon']
  let removed = myFish.splice(3, 1) 
  
  // myFish is ["angel", "clown", "drum", "sturgeon"]
  // removed is ["mandarin"] 
  ```
  
  ### `.forEach()`
  Iterates through an array and applies the callback function to each element.
  
  ```javascript
  let myArray = [1, 2, 3];
  
  // if array is even, add 100 to element
  myArray.forEach((element, index, array) => {
    if(element % 2 === 0) {
      array[index] += 100;
    }
  })
    
  console.log(myArray)
  \\\\ [1, 102, 3]
  ```
  
  - the callback function for `.forEach()` takes the parameters:
    -    current array element element
    -    index of the current element
    -    the entire array
  
  - it returns `undefined`
  - there is no way to `break` from it
  - usually an anonumus function is used but you can pass the name of an already defined function too
  
  ### `.map()`
  Invokes a callback function for each element of an array and returns a a new array.
  ```javascript
  const names = ['David', 'Richard', 'Veronika'];
  const nameLengths = names.map(function(name) {
    return name.length;
  });
  ```
  
  ### `.filter()`
  [Array.prototype.filter() - JavaScript \\| MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)
  Uses the callback function as a test and creates a new array from the elements that passed the test.
  ```javascript
  const names = ['David', 'Richard', 'Veronika'];
  const shortNames = names.filter(function(name) {
    return name.length < 6;
  });
  ```
  
  
  
  ## `spread` operator (`...`)
  
  The **spread oparator** `...` gives you the ability to expand, *spread* itarable objects into multiple elements.
  
  ```javascript
  const books = ['The Hobbit', 'Alice in Wonderland'];
  console.log(...books);
  
  const fruits = ['apples', 'kiwis'];
  const vegetables = ['peppers', 'tomatoes'];
  const produce = [...fruits, ...vegetables];
  
  ```
  
  ## `rest` parameter (`...`)
  
  The rest operator `...` allows you to represent an indefinite number of elements as an array.
  
  ```javascript
  const order = [20.17, 18.67, 1.50, "cheese", "eggs", "milk", "bread"];
  const [total, subtotal, tax, ...items] = order;
  console.log(total, subtotal, tax, items);
  // 20.17 18.67 1.5 ["cheese", "eggs", "milk", "bread"]
  
  
  const myPackage = ['cheese', 'eggs', 'milk'];
  console.log(...myPackage);
  // cheese egg milk
  ```
  
  Also works well for `variadic functions`. These are functions that can take an indefinite number of arguments.
  
  It used to work by using the `arguments object`.  The arguments object is an array like object that is available as a local variable in all funtions. It contains a value for each argument passed to the functions, at index 0 is the first argument and so on.
  ```javascript
  function sum() {
    let total = 0;  
    for(const argument of arguments) {
      total += argument;
    }
    return total;
  }
  ```
  The same functions with the `rest parameter`:
  ```javascript
  function sum(...nums) {
    let total = 0;  
    for(const num of nums) {
      total += num;
    }
    return total;
  }
  ```
  
  ### destructuring
  
  Destructuring values from an array:
  ```javascript
  const point = [10, 25, 7];
  
  const [x, y, z] = point;
  
  // you can also ignore values:
  const [x, , z] = point
  const [x, y] = point
  ```


FROM OTHER JS_ARRAY FILE:
array, js, javascript

# JavaScript Array
 
## Creation
 ```js
 // literal notation
 let myArray = ["bob", 3, {name: "rob", role: "admin"}];

 // with array constructor
 // new array lenght 4 is created
 let myArr = new Array(4);
```

 ## Destructuring

```js
// the second element of array is skipped and third element is assigned to location variable
let [empName, , location] = ["Shaan", 104567, "Bangalore"];
console.log(empName); // Shaan
console.log(location);  // Bangalore

// combined with rest operator
let [name, ...address] = ["Shaan", 104567, "Bangalore"];
console.log(name); // Shaan
console.log(address);  // [104567,'Bangalore']
```

## Iterate over with `for of`

```js
let names = ["bob", "rob", "mob"];

for(let name of names) {
    console.log(name);
}
```


## Array Methods

```js
// INSERT / DELETE : SPLICE

// splice(indexToInsertAt, # of charToRemove, stringToInsert)
let arr = ["a", "b", "c", "d"]

// insert at index
arr.splice(2, 0, "x");
console.log(arr) // ["a", "b", "x", "c", "d"]

// delete
arr = ["a", "b", "c", "d"]
arr.splice(1, 2);
console.log(arr); // ["a", "d"]

// insert & delete
arr = ["a", "b", "c", "d"]
arr.splice(1, 2, "y");
console.log(arr); // ["a", "y" "d"]
```

## ThinkOvers

WHat is the output?
```js
let myArr = [];
for (i = 0; i < 3; i++) {
    myArr.push(function () {
        console.log(i);
    })
}
for (j = 0; j < 3; j++) {
    myArr[j]();
}
```

This code will perform the following things.

1. In the first loop, it will push the function with console statement into an array, and at end of the loop, i value will be 3.

2. In second loop, `myArr[j]()` will invoke the function inside the Array and prints the value of i.

So the output will be 3 3 3.