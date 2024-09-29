JavaScript, js, scope

## Scope
>The scope is the current context of execution in which values and expressions are "visible" or can be referenced.

- global scope
    - the default scope
    - accessible from anywhere in the program

- ( module scope - do not need to know)

- function scope

- block scope
    - scope created with a pair of `{}`
    - only for `let` and `const`
- (lexical scope aka closure scope)


## Hoisting

- `var`-declared variable declarations and `function declarations` made with the function keyword are hoisted
- you can refer to the variable anywhere in its scope, even if its declaration isn't reached yet. 
- however, if you access a variable before it's declared, the value is always `undefined`, because only its declaration and default initialization (with undefined) is hoisted, but not its value assignment

## Closure

>A `closure` is the combination of a function and the lexical environment within which that function was declared.

This environment consists of any local variables that were in-scope at the time the closure was created.

Example:

```javascript
function makeFunc() {
  const name = "Mozilla";
  function displayName() {
    console.log(name);
  }
  return displayName;
}

const myFunc = makeFunc();
myFunc();
```

The instance of `displayName` maintains a reference to its lexical environment, within which the variable `name` exists. For this reason, when `myFunc` is invoked, the variable name remains available for use, and "Mozilla" is passed to console.log.

