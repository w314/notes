react

# React

> React is a JavaScript library to build front-end application.
- the view is the function of your application state
- uses components based architecture, it composes components together to create a view

- declarative (abstracted behind a declarative API), allows 

- allows these components to describe how the UI looks like from inside the view
- interprets separation of concerns differently
    - instead of seprating html-css-js
    - it wants it components to be able to describe the UI for commponent would look like inside the component
        - view and logic are together inside the component
        - uses `JSX` to describe the view


## Virtual DOM

React uses a Virtual DOM.  For every DOM object, react has a corresponding "virtual DOM object" that represents the actual DOM object.

Why?
<br>Manipulating the DOM is slow. Manipulating the virtual DOM is much faster because nothing gets drawn onscreen.

How?
<br>When you try to update the DOM in React:
- The entire virtual DOM gets updated.
- The virtual DOM gets compared to what it looked like before you updated it. (the snapshot) 
- React figures out which objects have changed.
- The changed objects, and the changed objects only, get updated on the real DOM.
- Changes on the real DOM cause the screen to change.

## JSX

## Create a React App
```bash
#  if using with TypeScript
npx create-react-app <app-name> --template typescrpipt

# create TypeScirpt config file if needed
npc tsc --init

#  install dependencies if using cloned directory
npm install

# start react app
npm start
```

- React Apps can have devDependencies installed with: <br>`npm i --save-dev <dependecy-name>`
- To work with TypeScript you need the type definition for the React library that can be installed with: <br> `npm i --save-dev @types/react`

## React Component
> React component is reusable piece of UI
- can be class or function based 

- a javaScript function that returns a UI
- if you encapsulate it in a module you can export it and import it wherever you need it
- you do not invoke it as a regular function but treat it as it were an HTML elment
    - Use Pascal Case for component name, it diffrentiates it form a normal DOM element
    - `<footer />` HTML element
    - `<Footer />` React element

- follow the single responsibility principle when creating components

TypeScript Component
```ts
// components is stored in ChildComponent variable
// it's type:
// React.FunctionComponent<{
//   prop1: string,
//   prop2: number
// }>
const ChildComponent:React.FunctionComponent<{
    name: string,
    count: number
}> = (props) => {
    return(
        <>
            <h2>I am a Child Component</h2>
            <ul>My Props:</ul>
            <li>Name: { props.name }</li>
            <li>Count: { props.count}</li>
        </>

    )
}
// component is exported to be used elsewhere
export default ChildComponent;
```
- type of the component is `React.FunctionComponent<{prop object}>`
- the component is a function with a props object as the argument
- it return a description of the UI

class based syntax:
```js
import React from 'react'

class Hello extends React.Component{
    render(){
        return <p>Hello World!</p>
    }
}
```


## Hooks
>Hooks are functionsthat let you “hook into” React state and lifecycle features from function components.
- are at the top of the component similar to how you import modules at the top the file
- there cannot be inside a conditional statement
- not for class based components
- there are built-in hooks and you can build custom ones too

### useState
- is a hook that allows you to persist a value across renders and trigger a re-render when the value changes
```tsx
// useState returns a two element array
// here we use array destructuring to store them
const [count, setCount] = React.useState(0)
```
- takes in a single argument, the initial value for that piece of state
- returns an array:
    - first item is the state value
    - second item is a function to update that state


How to use useState:
```tsx

```
### useEffect

### useNavigate

### useContext


## Routing
>Routing allows for the navigation from one view to another, by changing which components are displayed on the single page.

- What components are shown is determined by the URL 
- Certain components will be linked (or ROUTED) to certain URL endpoints

### React Router
>React Router is a declarative model for navigational components within your application.

Not part of the React library, to use React Router Dom install it with:
```bash
npm install react-router-dom
```

To use Routing in our app:
```tsx
// imports needed for routing
import { BrowserRouter, Route, Routes } from 'react-router-dom';

function App() {
  return (
    <div className="App">
        <BrowserRouter>
            <Routes>
                <Route path="/hyp" element={<Hypotenuse/>}></Route>
                <Route path="/emp" element={<EmployeeContainer incomingData={data}/>}></Route>
            </Routes>
        </BrowserRouter>
    </div>
  );
}

export default App;
```

### `<Link>`
