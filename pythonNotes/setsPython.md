createdAt: "2019-08-21T13:32:55.633Z"
updatedAt: "2020-07-07T19:17:03.124Z"
type: "MARKDOWN_NOTE"
folder: "68038d270558e5b040df"
title: "Python Sets"
tags: [
  "set"
  "python"
]
content: '''
  # Python Sets
  - sets are **unordered** and **mutable** collections
  - sets can only have unique elements
  - (sets are available in javascript ES6, but they are ordered unlike in python)
  
  
  ### Creating a set
  Duplicate items present at set creation will be removed as the set is created.
  ```python
  colors = {'green', 'green', 'blue', 'red'}
  colors
  # {'blue', 'green', 'red'}
  ```
  To create an empty set:
  ```python
  my_set = set()
  ```
  Cannot create an empty set with `my_set = {}`, python will create an **empty dictionary**.
  
  ### Convert list to a set
  Use `set()` function for this type conversion.
  Duplicate elements are removed.
  
  ```python
  color_list = ['red', 'green', 'blue', 'blue']
  
  color_set = set(color_list)
  color_set
  # {'blue', 'green', 'red'}
  ```
  
  ### Set Methods
  
  - add element - `add()`
  Nothing happens when trying the add an element already in the set.
  ```python
  color_set = {'blue', 'green', 'red'}
  
  color_set.add('yellow')
  color_set
  # {'blue', 'green', 'red', 'yellow'}
  
  color_set.add('yellow')
  color_set
  # {'blue', 'green', 'red', 'yellow'}
  ```
  
  - remove element - `remove()`
  ```python
  color_set = {'blue', 'green', 'red'}
  
  color_set.remove('red')
  color_set
  # {'blue', 'green'}
  
  color_set.remove('yellow')
  # KeyError: 'yellow'
  ```
  - remove random element - `pop()`
  
  - verifying if element is in set - `in` 
  ```python
  color_set = {'blue', 'green', 'red'}
  
  'blue' in color_set
  # True
  
  'yellow' in color_set
  # False
  ```
  
  
  
  ### Mathematical Operations
  
  - intersecion of two sets - `&`
  ```python
  color_set_1 = {'red', 'blue'}
  color_set_2 = {'blue', 'green'}
  
  common_colors = color_set_1 & color_set_2
  common_colors
  # {'blue'}
  ```
  
  - use `union()` to get the union of two sets
  ```python
  color_set_1 = {'red', 'blue'}
  color_set_2 = {'blue', 'green'}
  
  all_colors = color_set_1.union(color_set_2)
  all_colors
  # {'blue', 'green', 'red'}
  ```
  
  - use `issubset()` to check if one set is a subset of another
  Returns also True if the two sets have the same elements
  ```python
  color_set_1 = {'red', 'blue', 'green'}
  color_set_2 = {'blue', 'green'}
  
  color_set_2.issubset(color_set_1)
  # True
  ```
  
  - use `issuperset()` to check if one set is a superset of another
  Returns also True if the two sets have the same elements
  ```python
  color_set_1 = {'red', 'blue', 'green'}
  color_set_2 = {'blue', 'green'}
  
  color_set_1.issuperset(color_set_2)
  # True
  ```
  
  
  - use `difference()` to find elements only belonging to one set but not the other
  ```python
  color_set_1 = {'red', 'blue', 'green'}
  color_set_2 = {'blue', 'green'}
  
  unique_color_set_1_colors = color_set_1.difference(color_set_2)
  unique_color_set_1_colors
  # {'red'}
  ```
  
  
  
  
  
  
'''
linesHighlighted: [
  84
  85
]
isStarred: false
isTrashed: false
