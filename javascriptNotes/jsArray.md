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