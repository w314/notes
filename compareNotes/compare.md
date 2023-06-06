awcompare, python, py, js, javascript

# Compare

## number to sring
python:
```python
n = 232
s = str(232)
```
javascript:
```javascript
const n = 232
const s = n.toString()
```
## string to array of chars
python:

```python
s = 'abc'
l = list(s)   
# ['a', 'b', 'c']
```
```javascript
const s = 'abc'
const a = s.split('')
```

## `reduce` calculate sum of array

python
```python
import functools
import operator

l = [1, 2, 3]
# SOLUTION A
s = functools.reduce(lambda a, b: a + b, l)
# SOLUTION B
s1 = functools.reduce(operator.add, l)
```
javascript
```javascript
a = [1, 2, 3]
s = a.reduce((acc, curr) => acc + curr, 0)
```

# array: map
- returns new object

python
```python
l = ['1', '2']
# to get a list back and not a map object wrap it in list()
nl = list(map(lambda x: int(x), l))
# [1, 2]
```
javascript
```javascript
a = ['1', '2']
na = a.map(c => parseInt(c))
// [1, 2]
```