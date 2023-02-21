react, useContext, hooks

# React useContext() hook
- context is to pass down props to all the children component in an App without passing down props to every single one of them

## 1. Create context
```jsx

```

## The `Provider`
- Every context created by `createContext` has a provider.
- You have to wrap every component you want to access the conext into the provider
```javascript
<MyContext.Provider value={myData}>
</MyContext.Provider>
```
- Provider has a single property, the `value`, that has the value of the conext.
- All child components will have access to the value of the variable in `value`

## How to use context in a component
```jsx
// import useContext
import { useContext } from 'react'
// import context you wan to use
import { MyContext } from './ThemeContext'

export default function MyFuncti
onComponent {
  // use variables from context
  const myContextVar = useContext(MyContext)
}
```

You can get data passed to child components via props:
```typescript
import React from 'react'
import { useState } from 'react'


const PokemonFilter: React.FunctionComponent<{
  filter: string,
  setFilter: (value: string) => void,
  }> = ({filter, setFilter}) => (
    <input type="text" value={filter} onChange={(event) => setFilter(event.target.value) }></input>
)

function App() {
  const [filter, setFilter] = useState('')

  return (
    <div>
      <PokemonFilter 
        filter={filter}
        setFilter={setFilter}
      />
  )
}

export default App
```


## Why use context?
- passing data as props to components may mean that a lot of components have to deal with props they themselves don't need. (If useState is in App.tsx and the component that needs the data is several component layer down for example.)
- As app needs to know the props of the child component to call it, so you cannot change the implementation of the child component without changing App.tsx


## useContext() solution 