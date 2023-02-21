useReducer, react, hooks

# useReducer()

Resources:
- [web dev simplified](https://www.youtube.com/watch?v=kK_Wqx3RnHk&t=482s)
- [my counter project](https://github.com/w314/reactUseReducerExample)


## Steps to create the state with `useReducer`

### Create readucer
- a reducer is a function that takes a state and an action
  - state is the current state
  - action is an object that defines the mutation that is to be applied to the state
  - the reducer does the required mutation to the state and returns the new state


```jsx
import { useReducer } from 'react'


const pokemonReducer = useReducer(state, action) => {
  switch(action.type) {
    case 'oneAction':
      // do stuff
      // return new state
    default:
      throw new Error()
  }
}