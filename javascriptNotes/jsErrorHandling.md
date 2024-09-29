# JavaScript Error Handling
  
  ## `Try/Catch`
  
  ```javascript
  try {
     let two  = 2
     let result = two - "one";
     console.log(`I am succesfull`)
  } catch (err) {
     console.error(err.message);
  } finally {
     console.log('I run last');
  }
  ```
  - 2 - 'one' results in `NaN`
  - function is succesfull and will console "I am succesfull"
  - even in strict mode NaN, Null, undifened never generate errors
  - Catch won't catch them
  - have to build in custom error handling

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
