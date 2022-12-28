js, javascript, object_restructuring, spread_operator 

## Object Destructuring
- [Object Restructuring](https://www.youtube.com/watch?v=NIq3qLaHCIs&t=0s)

### Array Destructuring
- use `[]` when destructuring
- destructuring is based on position within the array



Destructure arrays
```javascript
const alphabet = ['a', 'b', 'c', 'd', 'e']

const [A, , C, ...rest] = alphabet

console.log(A)  // a
console.log(C)  // c
console.log(rest) // ['d', 'e']
```

Destructure function returns
```javascript
  function sumAndMultiply(a, b) {
    return [a + b, a * b]
  }

  const [sum, multiple] = sumAndMultiply(2, 3)

  console.log(sum) // 5
  console.log(multiple)  // 6

  // possible to set default values in case the function doesn't return a value
  const[s, m, div = 'no division'] = sumAndMultiply(2, 4)

  console.log(s) //6
  console.log(m)  // 8
  console.log(div) // 'no division'
```

### Object Destructuring
- use `{}` when destructuring
- based on key names

```javascript
personTwo = {
  name: 'Sally',
  age: 32,
  address {
    city: 'SomeCity',
    state: 'SomeState'
  }
}

const { name, age } = personTwo

console.log(name) // 'Sally'
console.log(age)  // 32

// you can change name of variable
const { name: firstName } = personTwo
console.log(firstName)  // 'Sally'

// use defaults
const { pet = 'snake'} = personTwo
console.log(pet)  // 'snake'


// use the spread operator
const { name: lastName, ...rest}
console.log(rest)
// { age: 32, address { city: 'SomeCity', state: 'SomeState'}}


// destructure nested object
const { age: yourNumber, address: { city } } = personTwo
console.log(city) // 'SomeCity'
```

Combine object
- new object will have keys from all objects combined
- values with same key names will be overwritten with later value
``` javascript
const personOne = {
  name: 'Bob',
  pet: 'snake',
}

const personTwo = {
  name: 'Bobek',
  color: 'beige'
}

const personMixed = {...personOne, ...personTwo}
console.log(personMixed)
// {name: 'Bobek', pet: 'snake', color: 'beige'}
```

Object destructuring in function parameters
```javascript
const person = {
  name: 'Bob',
  pet: 'mouse',
  age: 3,
  color: 'pinkish'
}

// use {} for object destructuring
function printPerson({name, age, pet='snake'}) {
  console.log(`Name: ${name}, age: ${age}, pet: ${pet}`)
}

printPerson(person)
```
<hr/>

### Spread Operator
- concatenate arrays
```javascript
const abc = ['a', 'b', 'c']
const nums = [1, 2, 3]

const mixed = [...abc, ...nums]

console.log(mixed)
// ['a', 'b', 'c', 1, 2, 3]

// can be done with
const mixed1 = abc.concat(nums)
console.log(mixed1)
// ['a', 'b', 'c', 1, 2, 3]
```