js, map

# JS Map

```js
const map = new Map();
map.set('a', 1);
map.set('b', 2);
const aValue = map.get('a');
const mapSize = map.size;
map.delete('b');

// getting non-existence key returns undefined
console.log(map.get('c')); // undefined

