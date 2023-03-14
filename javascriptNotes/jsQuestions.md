## Primitives
- are immutable
- are passed by value


## Strings

###  interpolation
Replacing a variable with its value in a string.
```javascript
const name = 'Bobek';
console.log(`Hi ${name}!`) // Hi Bobek!
```

### `.at()` method
Reads the charactor of a string at a certain index. Can be used with negativ numbers
```js
const name = 'Bobek'
const char = name.at(-2)  // e

// [] CANNOT be used with NEGATIVE indexes
name[-2] // undefined
```

# Data Structures
### Array
- ordered collection of elements
- elements are referenced by a numeric key called `index` that starts from zero and increments by one for each additional element of the array

### Objects
- collection of key-value pairs

# Objects
## Object
- data structure: collection of key-value pairs
- keys the names of the object properties are strings
- objects can `take a function` as `property value`
  - these properties are called `methods`
  - have access to the properties of their parent object with the `this` keyword  
```js
// creating object using literal notation
const dog = {
  name: 'doggy',
  color: 'tan',
  bark: function() {console.log('wuf')}
}

// data within objects are mutable
dog.color = 'white'

// properties can be added
dog.numLegs = 4

// properties can be removed
delete dog.color


```

## Prototypal inheritace
- JS object based system is based on `prototypes` not `classes`.
### Difference between Class & Prototypal Inheritance
#### Class Inheritance
- class is like a blueprint, a description of the object to be created
- classes inherit from classes and create subclass relationships

### Prototypal Inheritance
- there are no classes in JS, consturctor function are used even if `class` is used
```js
class Foo {}
typeof(Foo) // function
```
- inheritance uses the protoype chain: the 
