# Sort

## Sort array
> `sort()` sorts array alpahbetically

## Sort strings
Mutate array in place:
```javascript
const strings = ['d', 'a', 'b' ];
strings.sort()
// sort in descending order
strings.sort().reverse()
```
Sort and save sorted array into new variable
```javascript
const sorted = [...strings].sort()
```
- use the `...` `spread` syntax to make a copy of the array before sorting

## Sort numbers
```javascript
const nums = [3, 4, 18, 1, 8]

nums.sort((a, b) => { return a - b})
// sort in descending order
nums.sort((a, b) => { return b - a})
``` 
- provide compare function, if the result is negative a comes before b