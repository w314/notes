javascript, js, array, shallowCopy

# [Shallow Copy of an Array](https://developer.mozilla.org/en-US/docs/Glossary/Shallow_copy)

- if you change the value of a porperty of a member of the shallow object the original will change too
- if you reassign the value of a member of of the shallow copy array the original will NOT change

| All standard built-in object copy operations create shallow copies
- [spread syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax)
- [Array.prototype.concat()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/concat)
- [Array.prototype.slice()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/slice)
- [Array.from()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
- [Object.assign()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign)
- [Object.create()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create)

```javascript
// original array
let ingredients_list = ['noodles', {list: ['eggs', 'flour']}]

// shallow copy
let ing_list_copy = Array.from(ingredients_list)
console.log(JSON.stringify(ing_list_copy))

// CHANGING THE VALUE OF A SHARED PROPERTY OF AN EXISTING ELEMENT
ing_list_copy[1].list = ['rice flour', 'water']
console.log('ing_list_copy:')
console.log(JSON.stringify(ing_list_copy))

// !!! THE ORIGINAL ARRAY CHANGES TOO !!!!
console.log('ingeredients_list:')
console.log(JSON.stringify(ingredients_list))

// REASSIGNING THE VALUE OF AN ELEMENT
ing_list_copy[0] = 'rice_noodles'
console.log('\ning_list_copy:')
console.log(JSON.stringify(ing_list_copy))
// the origianal array is not affected
console.log('ingredients_list:')
console.log(JSON.stringify(ingredients_list))
```