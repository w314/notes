createdAt: "2019-08-19T18:05:22.878Z"
updatedAt: "2020-02-07T20:11:59.846Z"
type: "SNIPPET_NOTE"
folder: "68038d270558e5b040df"
title: ""
tags: [
  "variables"
  "javascript"
  "python"
]
description: ""
snippets: [
  {
    linesHighlighted: []
    name: "Variables in Python.md"
    mode: "Markdown"
    content: '''

  # Variables
  
  ## Variable Types

  ### JavaScript
  - `string`
  - `number`
  - `bigint`
  - `boolean`
  - `symbol`
  - `object`
  - `undefined`
  - `null`


  ### Python
  built-in data type in python:
  - Text Type: `str`
  - Numeric Types: `int`, `float`, `complex`
  - Sequence Types: `list`, `tuple`, `range`
  - Mapping Type: `dict`
  - Set Types: `set`, `frozenset`
  - Boolean Type: `bool`
  - Binary Types: `bytes`, `bytearray`, `memoryview`
  - float
  - str
  - boolean (True / False)
  
## Assignment

### Python

```python
x, y, z = 'bob', 'bobek', 'bunny'

x = y = z = 3

# unpacking
names = ['bob', 'bobek', 'bunny']
x, y, z = names
```

  ## Uninitialized variables

  ### JavaScript
  Unintialized varaiables have the value `undefined`.
```javascript
  let a;
  console.log(a);
  // undefined

  console.log(a + 2);
  // NaN

  console.log(a + 'BOB');
  // undefinedBOB
  ```

  ### Python
  In python variables are created when you assign a value to them, there is no command for declaring a variabled, therefore a variable cannot be unassigned.




  ## Determine Variable Type

  ### Python
  ```python
  type(True)
  # bool
  
  type(1) 
  # int
  
  type(1.0)
  # float
  ```
  
  
## Type Casting
If you want to specify the data type of a variable it can be done by casting.

### Python
```python
x = float(2)
# 2.0

y = int(1.7)
# 1

z = int('1')
#  1

a = int('a')
# ValueError: invalid literal for int() with base 10: 'a'

b = int(True)
# 1

c = int(False)
# 0

d = float(True)
# 1

e = float(False)
# 0

f = str(1)
# '1'

g = str(4.67)
# '4.67'

h = bool(1)
# True

i = bool(0)
#  False
```

## Global Variables
- Variable declared outside of a function is global.
- To create a global variable within a function:
### Javascript
- create a variable without `let` or `const`
### Python
- declare a variable `global` if you want to create a global variable within a function or if you want to change a global variable within a function
```python
# declare global variable inside a function
def my_func():
  global x
  x = 'bob'

# change global variable inside a function
x = 'bobek'
def other_func():
  global x
  x = 'bob'
```


## Mathematical Operations

### Python
- float division:
```python
25 / 5
# 5.0
```

- integer division:
```python
25 // 6
# 4
```

## Checking the Specifics of Float in the Runtime Environment

```python
import sys
sys.float_info
```
