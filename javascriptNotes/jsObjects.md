# Objects

Object Literal Notation:

```js
let myDog = {
    //state
    name: "Roger",
    color: "white",

    behavour
    bark: function() {
        console.log("wuff");
    }
}

// OR
const name = "Roger";
const color = "white";

let myDog1 = {
    name: name,
    color: color
}

// OR as the property and the value identifier have the same name SHORTHAND can be used
let myDog2 = {name, color};
```

## Dynamic properties
`Hash notation` can be used to add dynamic properties.
```js
const name = "bob";
const dynamicProperty = "age";

let myDog = {
    name,
    [dynamicProperty] = 3
}

console.log(myDog.age) //3
```

## Function Constructor
> Used to construct multiple objects with the same set of properties and methods.

- can be invoked with the `new` keyword
- basically replaced with new `class` syntax

## Spread Operator
- used to clone objects
- used combine objects

```js
let myObj1 = {
    name: "bob";
}

// creates clone/copy of myObj1
let myObj2 = {
    ...myObj1;
}

// content is the same
console.log(JSON.stringify(myObj1) === JSON.stringify(myObj2)) // true
// objects are not equal
console.log(myObj1 === myObj2)

let myObj3 = {
    pet: "dog";
}

// merges myObj1 & myObj3
let myObj4 = {
    ...myObj1,
    ...myObj3
}
```

## Object Destructuring

> Syntax to extract properties from objects to store them into vairables.

```js
let myObject = { name: 'Arnold', age: 65, country: 'USA' };

// alias can be used with : 
let { name, age:currentAge } = myObject; 
console.log(currentAge); // 65 

// use select propert only as parameter
function showDetails({ country }) { 
    console.log(country); 
} 

showDetails(myObject); 
```

## Accessing Object Properties

```js
let person = {name:"bob", pet:"dog"};

// dot notation
console.log(person.name)
// bracket notation
console.log(person["name"])
let property = "pet"
console.log(person[property]); // dog
```

## for in loop
```js
let person = {
    name: "bob",
    age: 3,
    pet: "dog"
}

for(let key in person) {
    console.log(key); // name, age, pet
    console.log(person[key]); // bob, 3 dog
}
```

## SEE also file jsGlobalObjects.md
