createdAt: "2021-01-12T17:17:11.067Z"
updatedAt: "2021-01-12T17:25:38.861Z"
type: "MARKDOWN_NOTE"
folder: "7869a5810e7871ff4be9"
title: "JavaScript Error Handling"
tags: []
content: '''
  # JavaScript Error Handling
  
  
  ## `Try/Catch`
  - even in strict mode NaN, Null, undifened never generate errors
  - Catch won't catch them
  - have to build in custom error handling
  ```javascript
  try {
     let two = 2
     two - 'fifteen'
     console.log(`I am succesfull`)
  } catch (err) {
     console.error(err.message);
  } finally {
     console.log('I run last');
  }
  ```
  - two - 'fifteen' results in `NaN`
  - function is succesfull and will console "I am succesfull"
  
  Solution:
  ```javascript
  try {
     // undeclared variable being used in an operation causes an error
     let two = 2
     let result = two - 'fifteen'
     if (Number.isNaN(result)) {{
        try {
          throw new Error('something is not right')
        } catch (err) {
          console.log(err.message);
        }
      }}
     console.log(`I am succesfull`)
  } catch (err) {
     console.error(err.message);
  } finally {
     console.log('I run last');
  }
  ```
'''
linesHighlighted: []
isStarred: false
isTrashed: false
