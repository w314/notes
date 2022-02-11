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

  some more notes:
  createdAt: "2021-02-02T17:46:02.320Z"
updatedAt: "2021-02-02T18:14:07.525Z"
type: "SNIPPET_NOTE"
folder: "096077ec96120ea00fda"
title: "Strings"
tags: [
  "string"
]
description: "Strings"
snippets: [
  {
    linesHighlighted: [
      3
      2
    ]
    name: "stringsJavaScript.md"
    mode: "Markdown"
    content: '''
      ## Strings
      - strings are `immutable`
      - value of a string can be changes, but individual characters of a string literal cannot be altered
      ```js
      // this works
      myString = 'Bob';
      myString = 'Bobek';
      
      // this does NOT work
      myString = 'Bob';
      mystring[0] = 'M'; // CANNOT BE DONE
      ```
      
      ## Concatenate strings
      ```js
      const whoseStuff = "my";
      const myString = "this is " + whoseStuff +  " stuff";
      
      
      // lenght of string
      const myString = 'Bob';
      console.log(myString.length);
      
      const firstLetter = myString[0];
      ```
      ## Escape characters
      - `\\'`
      - `\\"`
      - `\\\\`
      - `\\n` - new line
      - `\\r` - carriege return
      - `\\t` - tab
      - `\\b` - word boundary
      - `\\f` - form feed
    '''
  }
  {
    linesHighlighted: []
    name: "stringsPython.md"
    mode: "Markdown"
    content: '''
      ## String in Python
      - Textual data in Python is handled with `str` objects or strings in python. 
      - Strings are `immutable sequences` of unicode code points
      
      
      ## String manipulation
      
      ```python
      # length of string - use built in len() function:
      my_str = 'bob'
      print(len(my_str))
      
      firstLetter = my_str[0]
      
      ```
    '''
  }
]
isStarred: false
isTrashed: false

