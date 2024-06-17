react, context

# React Context API
> Used for state management. Provided a way to pass data through the component tree without passing props from component to component.


## Create Context

```tsx
export interface UserInterface {
    userId?: number,
    username: stirng,
    password: string,
    jwt?: stirng
}
```

```tsx

// CREATE CONTEXT
// defatul value for the global usre state objs

const initialState: UserInterface = {
    userId: 0,
    userName: "",
    jwt: ""
}

export const UserContext = React.createContext<{
    globalUserData: UserInterface
    // setter for global state it expects an UserInterface object
    setGlobalUserData: React.Dispatch<React.SetStateAction<UserInterface>> (
        {
            // setting inital value of state
            globalUserData: initialState,
            // placeholder for mutator function will be defined in the Provider
            setGlobalUserData: () => {

            }
        }
    )
}>

```


## Create Provider

Create Provider
```tsx
// CREATE PROVIDER - passes down (provides) the context to its children
export const UserProvider: React.FC<any> = ({children}) => {

    // define state with useState
    const [ globalUser, setGlobalUserData ] = useState<UserInterface>({
        userId: 0,
        username: "",
        jwt: ""
    })

    return (
        <UserContext.Provider value={{
            globalUserData,
            setGlobalUserData
        }}>
            { children }
        </UserContext.Provider>
    )
}
```

Provide provider in App.tsx
```tsx



```

## Use Context in Component
```tsx
const { globalUserData, setGlobalUserData } = useContext(UserContext)
```


## Exposing value but not setValue
you can make the value accessible but not the setValue function by creating two separate contexts: one for the value and one for the setValue function. Then, you can choose to provide only the value context to the components that should not be able to mutate the state. Here's an example:
```tsx
import React, { createContext, useState, useContext } from 'react';

// Create two Contexts
const ValueContext = createContext();
const SetValueContext = createContext();

function MyComponent() {
  // This component can mutate the context
  const value = useContext(ValueContext);
  const setValue = useContext(SetValueContext);

  return (
    <button onClick={() => setValue(value + 1)}>
      Increment
    </button>
  );
}

function MyReadOnlyComponent() {
  // This component can only read the context
  const value = useContext(ValueContext);

  return <div>Value: {value}</div>;
}

function App() {
  const [value, setValue] = useState(0);

  return (
    <SetValueContext.Provider value={setValue}>
      <ValueContext.Provider value={value}>
        <MyComponent />
      </ValueContext.Provider>
      <MyReadOnlyComponent />
    </SetValueContext.Provider>
  );
}
```