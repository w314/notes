react, hooks, useState

# useState React Hooks

Hooks can only be used with `function components`

## About `useState`
- you can use several of them in the function
- must be executed in the same order always => 
  - cannot put one within an `if` statement that may not run (or function or things like that)
  - must be defined as first thing in the function to run first

## How to use `useState`
### import useState

```javascript
import { useState } from 'react'
```
### call useState
  - parameter passed to useState() sets default state
  - **`useState` returns an array** with two values, the value of the current state and the function to set the state. We use `destructuring` to get the values of the array to two variables
```javascript
function App() {
  // TWO WAYS TO PASS DEFAULT STATE

  // 1. PASSING A VALUE
  /* this will run every time the component renders */
  const [count, setCount] = useState(4)

  // 2. USING A FUNCTION
  /* the function is run only the first time the component renders
  (similar to class components where state is set in the constructor which runs only once) */
  const [theme, setTheme] = useState(() => {return 'blue'} )
}
```

### update state
- call `setState()` to update the state
```javascript
const [count, setCount] = useState(4)

setState(9)

// USE PREVIOUS STATE
setstate(prevCount => prevCount + 1)

// WRONG WAY TO USE PREVIOUS STATE
// count will increase by 1 only
// as count equals 4 in both lines
function increaseByTwo() {
  setState(count + 1)
  setState(count + 1)
}
// USE FUNCTION FORM INSTEAD
// prevCount will be correct each time
// function works as intended
function increaseBy2() {
  setState(prevCount => prevCount + 1)
  setState(prevCount => prevCount + 1)
}

```



-  using an object to set state vs. several useStates() (in general: use several useStates() instead of using an object for state)
```javascript
const [state, setState] = useState({count: 4, animal: 'dog'})

// INCORRECT way to update state
setState( prevState => 
  { return { count: prevState.count + 1 } 
})
```
- the returned object will NOT be merged with the previous one (as it would in class components), but will OVERWRITE it and we lose our animal property

```javascript
// CORRECT way to update state
setState( prevState => {
  return { ...prevState, count: prevState.count + 1 }
})
````
- spread out prevState and then set new value of property involved



```javascript
import { useState } from 'react'

function App() {
  // parameter passed to useState() sets default state of count
  // this will run every time
  const [count, setCount] = useState(4)

}


```