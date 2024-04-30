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

## JSX vs HTML

### Basic Syntax
- wrap your return statement in `()` if you start your jsx on the next line, as js will put a `;` at the end of return and nothing will be returned
- you can only return 1 top-level element
    - can be any element
    - or `<React.Fragment></React.Fragment>`
    - or `<></>` shorthand for React.Fragment

- close you self closing tags wiht `/>` like `<input />` instead of `<input>`

- watch your attribute names
    - use `className` for `class` (class is a reserved word in js)
    - use `htmlFor` for `for`
    - convert them to camelCase `strokeWidth` instead of `stroke-width`
- wrap you js expressions in `{ }` 
    - called `Data Binding`
    - uses js to evalute the expression within `{ }`
- if you want to return nothing return `null`

### Conditional Rendering

- can do with `if - else` statements
- can do using `ternary` operators
```js
function Dashboard () {
  return isAuthed() === true
    ? <h1>Welcome back!</h1>
    : <h1>Login to see your dashboard</h1>
}
```

- can use the logical AND operator `&&`
```js
if (user && authed) {
  // runs if user and authed are truthy
}
```
        - only runs if both user and authed are truthy
        - if user is falsy authed is NOT checked

### Rendering Lists
- uses javascript's map method
- each list item need a unique `key` prop

```jsx
return (
    <ul>
        {users.map(user => (
            <li key={user.id}>{user.name}</li>
)       ))}
    </ul>
)

```
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

## TypeScript Component
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

## Props
Is an object passed as from parent component to child component

- props to components are like arguments to functions

### How to pass props
```jsx
<Profile
  username="tylermcginnis"
  authed={true}
  logout={handleLogout}
  header={<h1>👋</h1>}
/>

// can even pass object literals
<DatePicker settings={{
  format: "yy-mm-dd",
  animate: false,
  days: "abbreviate"
}} />

// bolean shortcut
<Profile authed={true} />
// is the same as
<Profile authed />
```
- passing them as attributes on the Component
- if not passing a string enclose in `{ }`
- use `{{ }}` when passing object literals
- props without a value evalutate to `true`

### Accessing Props
React will put all of the props on an object, and pass that object as the first argument to the function.

Regardless of how many props you pass to a component, each prop is added as a key on the props object.
```js
function Hello (props) {
  return (
    <h1>
      Hello, {props.first} {props.last}
    </h1>
  )
}

export default function App () {
  return <Hello first="Tyler" last="McGinnis" />
}
```
And because props is just an object, you can also destructure it if you'd like.

```js
function Hello ({ first, last }) {
  return (
    <h1>
      Hello, {first} {last}
    </h1>
  )
}
```

### `props.children`
Whatever is between the opening and closing tag of an element will be accessible inside of the component via `props.children`.


## State in React
State stores information within a component.

## React Data Flow

### Lifting state
Whenever you have state that multiple components depend on, you'll want to lift that state up to the nearest parent component and then pass it down via props.
- the passed down state is read-only


### Child "updating" state in parent component
- when lifting state up you may decouple where the state lives from the event handlers that update that state.
- to solve this, you'll create an updater function in the parent component where the state lives and, via props, invoke that function from the child component(s) where the event handler(s) live.

```jsx
import * as React from "react";
import Todo from "./Todo"

// PARENT COMPONENT
import * as React from "react";
import Todo from "./Todo"

export default function TodoList() {
  const [todo, setTodo] = React.useState({
    id: 1,
    label: "Learn React",
    completed: false,
  })
    
  const handleUpdateTodo = (updatedTodo) => {
    setTodo(updatedTodo)
  }

  return (
    <ul>
      <Todo
        // passing todo object
        todo={todo}
        // passing function that updates the state
        handleUpdateTodo={handleUpdateTodo}
      />
    </ul>
  )
}


// CHILD COMPONENT
import * as React from "react"

// getting todo object and updater function as props
export default function Todo ({ { todo, handleUpdateTodo }}) {
 
  // event handler for checkbox click
  const handleCheckboxClick = () => setTodo({
    ...todo,
    completed: !todo.completed
  })
  
  // when checkbox is clicked we do not update state in todo (we do not have one here) 
  // our event handler will call  the updater function passed as props
    const handleCheckboxClick = () => handleUpdateTodo({
        // we use spread syntax to update the object
    ...todo,
    completed: !todo.completed
  })

  // our checkbox would look like
            <input
            type="checkbox"
            id={todo.id}
            checked={todo.completed}
            // we attach the event handler here
            onChange={handleCheckboxClick}
          />

```



### Parent to Children Data FLow
- parent component passes read-only properties to child component

### Child to Parent Component
- if a child has to change the a parent's state it will path a callback function to the child component
- the child component can use that callback function to change the state of it's parent component


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

- when passing object use te
### useEffect

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
>Helps to navigate between our routes.

The `to` attribute takes the path.

```jsx
<nav>
  <Link to="/">Home</Link>
  <Link to='/about'>About</Link>
</nav>
```