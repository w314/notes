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



class based syntax:
```js
import React from 'react'

class Hello extends React.Component{
    render(){
        return <p>Hello World!</p>
    }
}
```
## Virtual DOM

React uses a Virtual DOM. Technically, with React, you don't actually write HTML. Instead, you generate HTML views using JS. For every DOM object, react has a corresponding "virtual DOM object" that represents the actual DOM object.

Why is using a Virtual DOM useful? Updating the DOM is costly in terms of performance. React greatly improves performance by minimizing changes to the DOM - it only updates what's necessary. The Virtual DOM much more lightweight than the actual DOM, so the virtual DOM is updated whenever we make a change, but React will decide when it is most efficient to actually make the real DOM reflect the changes seen in the Virtual DOM. Since rendering the page is costly (performance wise), minimizing unnecessary renders is one way that React improves performance. This update process is referred to as reconciliation, and you can read more about it her


