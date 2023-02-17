react, useContext, hooks

# React useContext() hook

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