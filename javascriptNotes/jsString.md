# JavaScript String
> Wrapper object for primitive string.
- provides methods to manipulate the given text.
- provides length property

Methods:
- chartAt() - returns index
- concat()
- indexOf() - index of given character or string


## String Methods

```js
// SPLIT

// split() : string => array
let str = "my new dog";
let arr = str.split(" ");
console.log(arr);  // ["my", "new", "dog"]



// SUBSTRING

// with length
// substr(start, length)
str = "abcdefg";
let s1 = str.substr(2, 3);
console.log(s1); // cde 

// with start-end index
// substring(start, end)
str = "abcdefg";
let s2 = str.substring(2, 3);
console.log(s2); // c
