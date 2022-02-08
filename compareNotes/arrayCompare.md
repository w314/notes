# Arrays / Lists (Python)

## Add element to array

### Add element to the  **end** of the array

#### JavaScript `push()`

```javascript
let myArr = [1, 'cat'];
myArr.push([3, 'dog']);
```

#### Python `append()`

```python
my_arr = [1, 'cat']
my_arr.append([3, 'dog'])
```

### Add element to the **beginning** of the array

#### JavaScript `unshiftf()`

```javascript
let myArr = [1, 'cat'];
myArr.unshift([3, 'dog']);
```

#### Python `insert()`
- `insert()` inserts an item at the specified index
```python
my_arr = [1, 'cat']
my_arr.insert(0, [3, 'dog'])
```

## Remove and return element from array

### Remove and return last element of array `pop()`

#### JavaScript

```javascript
let myArr = [1, 'cat'];
let lastElement = myArr.pop();
```

#### Python `pop(index)`

```python
my_arr = [1, 'cat']
# by default returns last element
last_element = my_arr.pop()
# can use index to return any element
indexed_element = my_arr.pop(0)
```

### Remove and return **first** element of array

#### JavaScript `shift()`

```javascript
let myArr = [1, 'cat'];
let firstElement = myArr.shift();
```

#### Python `pop(0)`

```python
my_arr = [1, 'cat']
first_element = my_arr.pop(0)
```


form old boostnote note
createdAt: "2020-09-09T20:03:56.019Z"
updatedAt: "2021-06-01T20:23:10.772Z"
type: "MARKDOWN_NOTE"
folder: "5933e21a727916409ef5"
title: "Arrays"
tags: [
  "arrays"
  "python"
  "javascript"
]
content: '''
  # Arrays
  
  ## Get last element
  
  - python: `arr[-1]`
  - javascript: `arr[arr.length-1]`
  
  ## Swap two elements of the array
  
  #### python
  ```python
  arr[0], arr[1] = arr[1], arr[0]
  ```
  
  ### javascript
  ```javascript]
  
  const arrElement = arr[1];
  arr[1] = arr[0];
  arr[0] = arrElement;
  ```
  
  ## Merging two arrays
  ### python
  ```python
  a = [1, 2]
  b = [3, 4]
  a = a.extend(b)    # [1, 2, 3, 4]
  ```
  
  ### javascript
  ```javascript
  let a = [1, 2]
  let b = [3, 4]
  a = [...a, ...b]    // [1, 2, 3, 4]
  ```
  
  ## Slicing arrays
  
  ### python
  ```python
  arr = [1, 2, 3]
  arr[1:]    # [2, 3]
  ```
  ### javascript
  ```javascript
  let arr = [1, 2, 3]
  arr.slice(1,)    // [2, 3]
  ```
'''
linesHighlighted: [
  0
]
isStarred: false
isTrashed: false

from another old boostnote note
createdAt: "2021-02-05T17:27:43.216Z"
updatedAt: "2021-02-05T17:43:59.556Z"
type: "SNIPPET_NOTE"
folder: "096077ec96120ea00fda"
title: "Arrays"
tags: [
  "array"
]
description: "Arrays"
snippets: [
  {
    linesHighlighted: []
    name: "arraysJavaScript.js"
    mode: "JavaScript"
    content: '''
      let myArray = [1, 2, 3];
      
      // add element to array
      // add to the end
      myArray.push(4);  //[1, 2, 3, 4]
      // add to the beginning
      myArray.unshift(0);
      
      // remove and return element of array
      // lastElement
      const lastElement = myArray.pop();
      // firstElement
      const firstElement = myArray.shift();
      
      
      
      
    '''
  }
  {
    linesHighlighted: []
    name: "arrayPython.py"
    mode: "Python"
    content: '''
      #### LISTS ####
      # list are mutable ordered sequence of elements
      
      my_list = [1, 2, 3]
      
      # add to the end of array
      my_list.append(4)  # [1, 2, 3, 4]
      
      # delete and return element at index
      fist_element = my_list.pop(0)
      # if no index is provided the default is the last element
      last_element = my_list.pop()
      
      
      
      
    '''
  }
]
isStarred: false
isTrashed: false

