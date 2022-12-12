createdAt: "2020-03-24T16:55:36.553Z"
updatedAt: "2020-10-16T16:24:46.020Z"
type: "MARKDOWN_NOTE"
folder: "ae0700cca340ec1715f7"
title: "React"
tags: [
  "react"
  "yarn"
  "jsx"
]
content: '''
  # [React](https://reactjs.org/)
  
  - unlike `Angular`, `React` avoids the separation of rendering logic from other UI logic
  
  
  ## install react
  
  To install `react` in terminal run: `npm install -g create-react-app`
  This will install react globally on your computer
  To check for succesfull installation run: `create-react-app --version`
  
  ## start a react app
  - if using [Yarn - Package Manager](https://yarnpkg.com/) make sure it's installed (`npm` works as well),  it's a popular package manager, that works well with react
  - create a project directory and cd into it
  - with yourProjectName run: `create-react-app yourprojectname`
  Project name cannot have capital letters (npm rule).
  This will create a subfolder yourprojectname
  - move into the new subfolder
  - run `yarn start` (or `npm start`)
  if you need a different port you can change it in  `package.json`:
  ```js
  "scripts" : { 
    “start” : “set PORT 3001 && react-scripts start”
  }  
  ```
  
   ## basic setup of a react up
   
   - in the `public/index.html` file you can find:
   ```html
  <body>
    <div id="root"></div>
  </body>
   ``` 
   
   - the `div id="root"` is rendered by the `src/index.js` file:
   ```js
  import React from 'react';
  import ReactDOM from 'react-dom';
  import './index.css';
  import App from './App';
  
  ReactDOM.render(
    <React.StrictMode>
      <App />
    </React.StrictMode>,
    document.getElementById('root')
  );
   ```
  
  - based on the content of the `src/App.js`
  ```jsx
  import React from 'react';
  import './App.css';
  
  function App() {
    return (
      <div className="App">
          <p>Hello World!</p>
      </div>
    );
  }
  
  export default App;
  ```
  
  ### `JSX`
  - App.js uses `JSX` (JavaScript Extension)
    - jsx is a syntatic extensions to JavaScript
    - it enables us to express react elements using HTML like syntax
  - a react element defined in jsx
  ```jsx
  const element = (
    <h1 classsName = "greeting">
      Hello World
    </h1>
  );
  ```
    - will call react.createElemen function with 3 parameters:
    ```jsx
    const element = React.createElement(
      'h1',
      {className: 'greeting'},
      'Hello, World'
    );
    ```
    - which will create a corresponding JavaScript object:
    ```jsx
    const element = {
      type: 'h1',
      props: {
        className: 'greeting',
        children: 'Hello, World'
      }
    };
    ```
  
  ## configure react app
  
  ### using `bootstrap` with react
  - javascript based components of `bootstrap` cannot be used directly with react
  - but we can use `Reactstrap`, which is `bootstrap` configured for react
  #### install bootstrap
  - to insall bootstrap in project directory run `yarn add bootstrap` (or `nmp install --save bootstrap`)
  - run `yarn add reactstrap react-popper`
  
  #### configure bootstrap
  - in `src/index.js` add:
  ```js
  // add it  before the line importing `./index.css`
  // so that we can override standard bootstrap
  
  import 'bootstrap/dist/css/bootstrap.min.css';
  ```
  #### use bootstrap
  - to add a `Navbar`:
  -  in the `src/App.js` file add:
  ```js
  import { Navbar } from 'reactstrap';
  ```
  the `App` class:
  ```js
  
  ```
  
  ## Build with React
  
  
  ///////////// old notes down ///////////////
  
  - JSX has to be compiled to JavaScript. Transpiler like Babel can do it. Babel can be run through a buid tool like Webpack.
  - Facebook’s Create React App is good for the same purpose and can becsetup without initial configuration. 
  
  ## How to add google map
  
  - run `npm install --save react-google-maps`
  
  ## How to use react browser router
  
  •	in terminal run: `npm install --save react-router-dom`
  •	in index.js
  ```js
  import { BrowserRouter } from ‘react-router-dom’
  ```
  - enclose `<App />` like: `<BrowserRouter><App /></BrowserRouter>`
  
  - in App.js
  ```js
  import { Route } from ‘react-router-dom’
  ```
  
  o	use Route to render UI like:
  	<Route path=”/” render(() => {}) />
  	or
  	<Route path=”/” component=”{}” />
  
  •	wherever there is a link
  o	import { Link } from ‘react-router-dom’
  o	<Link to=”/”>New Destination</Link>
  
  Render UI with external data
  
  •	import API 
  o	import * as MyAPI from ‘./utils/MyAPI’
  
  •	to fetch external data add component lifecycle event:
  o	componentDidMount(){
    MyAPI.getAllData().then((data) => {this.setState({data})})
  }
  
  
'''
linesHighlighted: [
  100
]
isStarred: false
isTrashed: false
