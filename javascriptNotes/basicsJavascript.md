createdAt: "2021-01-29T17:55:40.350Z"
updatedAt: "2021-02-12T14:21:37.279Z"
type: "SNIPPET_NOTE"
folder: "096077ec96120ea00fda"
title: "Basics"
tags: [
  "operators"
  "data_types"
  "comments"
  "style_guide"
]
description: '''
  Basics
  
'''
snippets: [
  {
    linesHighlighted: [
      3
    ]
    name: "operatorPython.md"
    mode: "Markdown"
    content: '''
      ## Basics
      - documentation: 
        - [3.9.1 Documentation](https://docs.python.org/3/index.html)
        - [cppreference.com](https://en.cppreference.com/w/)
      - style guide [PEP 8 -- Style Guide for Python Code \\| Python.org](https://www.python.org/dev/peps/pep-0008/)
      - commnents:
      ```python
      # there are only one line comments
      ```
      
      ## Operators
      
      - `+`
      - `-`
      - `*`
      - `/` - Division
      - `%`
      - `**` - Exponentiantion
      - `//` - Divides and rounds down to the nearest integer
      - logical operator: `not`, and`, `or`
      
      
      ## Data Types
      
      - `in` - for integers
      - `float` - for decimal numbers
      ```python
      int x = 3
      # check type of variable
      print(type(x))
      ```
      - `bool` - True / False
      - `str` - strings
    '''
  }
  {
    linesHighlighted: []
    name: "basicsJavaScript.md"
    mode: "Markdown"
    content: '''
      ## Style
      - for variable name use *camelCase*
      
      - comments:
      ```js
      // one line comment
      
      /* multiple
      line 
      comment */
      ```
      
      ## Data Types
      - `undefined`
        - when varables are declared they have the initial value of `undefined`
        - if you do a mathematical operation on an `undefined` variable the result will be `NaN` *not a numbe*
        - if you concatenate a string with `undefined` you will get a literal string of `undefined`
      - `null`
      - `boolean`
      - `string`
      - `symbol`
      - `bigint`
      - `number`
      - `object`
      
      
    '''
  }
  {
    linesHighlighted: [
      0
    ]
    name: "basicsC.md"
    mode: "Markdown"
    content: '''
      ## Documentation
      [CppCoreGuidelines/CppCoreGuidelines.md at master · isocpp/CppCoreGuidelines · GitHub](https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md)
      [C++ Core Guidelines](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#c49-prefer-initialization-to-assignment-in-constructors)
      
    '''
  }
]
isStarred: false
isTrashed: false
