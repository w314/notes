sort python javascript py js

# Sort

## Python
```python
l = [3, 4, 5]
l_sorted = sorted(l)
```
- returns sorted list


## Javascript

```javascript
a = [100, 72, 3]
a.sort()
// returns [100, 3, 72]
```
- sorts array in place
- converts array elements to string before sorting
- doesn't work for numbers

To sor numbers
```javascript
a = [100, 72, 3]
a.sort((a, b) => a - b)
// [3, 72, 100]
a.sort((a, b) => b - a)
// [ 100, 72, 3]
```