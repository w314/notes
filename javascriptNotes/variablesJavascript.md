# JavaScript Variables and Scope
## Variables
  
  - When js variables are declared, they have an initial value of `undefined`.
  - If you do a mathematical operation on an `undefined` variable, your result will be `NaN`, wich means not a number.
  - If you concatenate a string with an `undefined` variable the result is `undefined`.
  
## Scope

`Scope` refers to the visibility of the variables.
- Variables defined outside of a function block have `global scope`.
- Variables created **without** the `let` or `const` keywords are automatically creaited in the `global scope`.
- Variables declared within a function as well as the function parameters have `local scope`