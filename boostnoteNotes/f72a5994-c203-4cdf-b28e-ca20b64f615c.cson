createdAt: "2019-08-19T16:12:10.163Z"
updatedAt: "2021-03-19T17:29:07.379Z"
type: "MARKDOWN_NOTE"
folder: "68038d270558e5b040df"
title: "Python 01 Variables & Operators"
tags: [
  "python"
  "variables"
  "operators"
  "divmod"
]
content: '''
  # Python 01 Variables & Operators
  ### Variable types
  - int
  - float
  - str
  - bool 
  `True`/ `False`
  - NoneType
  Only possible value: `None`, represents lack of a value
  
  ##### `int`
  ##### `float`
    - uses approximation, therefore:
  ```python
  0.1 + 0.1 + 0.1  == 0.3
  # False
  
  round(.1, 1) + round(.1, 1) + round(.1, 1) == round(.3, 1)
  # False
  
  round(.1 + .1 + .1, 10) == round(.3, 10)
  # True
  ```
  - checking the Specifics of Float in the Runtime Environment
  ```python
  import sys
  sys.float_info
  ```
  
  ##### `str`
  ##### `bool` 
  - `True` and  `False`
  
  ## Variable Assignment
  ```python
  x = 2
  y = 3
  
  # can be written as:
  x, y = 2, 3
  ```
  
  ## Determine Variable Type
  ```python
  type(True)
  # bool
  
  type(1) 
  # int
  
  type(1.0)
  # float
  ```
  
  
  ## Type Casting
  
  ### to `int`
  
  ```python
  # NO ROUNDING:
  int(1.7)
  # 1
  
  int('1')
  #  1
  
  int('a')
  # ValueError: invalid literal for int() with base 10: 'a'
  
  int(True)
  # 1
  
  int(False)
  # 0
  ```
  
  ### to `float`
  
  ```python
  float(2)
  # 2.0
  
  float(True)
  # 1
  
  float(False)
  # 0
  ```
  
  ### to `string`
  
  ```python
  str(1)
  # '1'
  
  str(4.67)
  # '4.67'
  ```
  ### to `bool`
  
  ```python
  bool(1)
  # True
  
  bool(0)
  #  False
  ```
  
  
  ## Arithmetic Operations
  
  - float division:
  ```python
  25 / 5
  # 5.0
  ```
  
  - integer division (rounds DOWN):
  ```python
  7 // 2
  # 3
  
  # NOTE!: 
  -7 // 2
  # -4 as it rounds down
  ```
  
  ### divmod
  Using `divmod` to convert integer to roman numbers
  ```python
  digits = [(1000, "M"), (900, "CM"), (500, "D"), (400, "CD"), (100, "C"), (90, "XC"), 
            (50, "L"), (40, "XL"), (10, "X"), (9, "IX"), (5, "V"), (4, "IV"), (1, "I")]
  
  def intToRoman(self, num: int) -> str:
      roman_digits = []
      # Loop through each symbol.
      for value, symbol in digits:
          # We don't want to continue looping if we're done.
          if num == 0: break
          count, num = divmod(num, value)
          # Append "count" copies of "symbol" to roman_digits.
          roman_digits.append(symbol * count)
      return "".join(roman_digits)
  ```
  
  ## Equality `==` vs. Identity `is`
  ```python
  a = [1, 2, 3]
  b = a
  c = [1, 2, 3]
  
  print(a == b)   # True
  print(a is b)   # True
  print(a == c)   # True
  print(a is c)   # False
  ```
  
  
  
  
  
  
'''
linesHighlighted: [
  14
  25
]
isStarred: false
isTrashed: false
