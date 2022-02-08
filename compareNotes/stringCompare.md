# Strings

## last character of a string

### JavaScript
```javascript
const myStr = 'Bobek';
const lastChar = myStr[myStr.length - 1];
```

### Python
```python
my_str = 'Bobek'
last_char = my_str[-1]
```

## Formating strings

### Python

  To use `formatted string literals`, begin a string with `f` or `F` before the opening quotation mark or triple quotation mark. Inside this string, you can write a Python expression between { and } characters that can refer to variables or literal values.
  
  ```python
  year = 2016
  event = 'Referendum'
  f'Results of the {year} {event}'
  #'Results of the 2016 Referendum'
  ```
  With the `str.format()` method
  ```python
  yes_votes = 42_572_654
  no_votes = 43_132_495
  percentage = yes_votes / (yes_votes + no_votes)
  '{:-9} YES votes  {:2.2%}'.format(yes_votes, percentage)
  ' 42572654 YES votes  49.67%'
  ```
