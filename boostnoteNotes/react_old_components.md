createdAt: "2020-09-14T16:20:04.460Z"
updatedAt: "2020-09-16T15:55:56.201Z"
type: "MARKDOWN_NOTE"
folder: "ae0700cca340ec1715f7"
title: "React Components"
tags: [
  "react"
  "component"
]
content: '''
  # React Components
  
  - a `component` returns a set of react elements that should appear on the screen
  - enables us to split the UI into independent resusable pieces
  - component accepts inputs
  - name of the component start with capital letter
    - it will compile to React.createElement(...)
  - tags starting with lowercase letters are treated as `DOM tags` 
    - these will trigger to use some of reacts's built-in componenst corresponding to these tags
  
  ## Compoments
  - receive `props` from parent component
  - `props` are immutable
  - under `src` create file `ListContacts.js`
  - in the `ListContacts.js` file:
  ```jsx
  import React, { Component } from 'react';
  
  class ListContacts extends Component {
  
      // first define constructor
      constructor(props) {
          // this line is required
          super(props);
      }
  
      // each class requires a render() method
      // this will return the view
      render() {
         return (
          <ol>
            <!-- access contacts property passed from app.js -->
            {this.props.contacts.map((contact, index) => (
              <!-- each <li> requires a key property -->
              <li key={index]}>
                {contact}
              </li>
            ))}
          </ol>
  
         );
      }
  }
  
  // need to export our component
  export default ListContacts;
  ```
  
  
  ## Stateless Functional Component
  - stateless component
  - useful if your component only has a render() method
  - under `src` create file `ListContacts.js`
  - in the `ListContacts.js` file:
  ```jsx
  import React, { Component } from 'react';
  
  function ListContacts(props) {
  
    return (
      <ol>
        <!-- access contacts property passed from app.js -->
        {props.contacts.map((contact, index) => (
          <!-- each <li> requires a key property -->
          <li key={index]}>
            {contact}
          </li>
        ))}
      </ol>
    )
  }
  
  // need to export our component
  export default ListContacts;
  ```
  - to use the new component in `src/App.js`:
  ```jsx
  import React, { Component } from 'react'
  import ListContacts from './ListContacts'
  
  // list of contacts array
  const contacts = ['Bob', 'Bobek']
  
  class App extends Component {
   render() {
    return (
      <div>
        <!-- passing list of contact -->
        <ListContacts contacts={contacts}/>
      </div>
    )
   }
  }
  ```
  
  ## State
  
  ### Adding `state` to a component
  ```js
  // with the help of Babel it can be than like this:
  
  class User extends React.Component {
    state = {
      username: 'Tyler'
    } 
  }
  
  // rather than the official version
  
  class User extends React.Component {
    constructor(props) {
      super(props);
      this.state = {
        username: 'Tyler'
      }
    }
  }
  ```
  
  - add state to App.js
  ```jsx
  class App extends Components {
    state = {
      contacts: ['Bob', 'Bobek']
    }
    
    render() {
      return(
        <div>
          <ListContacts contacts={this.state.contacts} />
        </div>
      )
    }
  
  }
  
  ```
  
  
  ⚠️ Props in Initial State ⚠️
  When defining a component's initial state, avoid initializing that state with props. This is an error-prone anti-pattern, since state will only be initialized with props when the component is first created.
  ```js
  // DO NOT DO THIS!!!!
  this.state = {
    user: props.user
  }
  ```
  In the above example, if props are ever updated, the current state will not change unless the component is "refreshed." Using props to produce a component's initial state also leads to duplication of data, deviating from a dependable "source of truth."
  
  
  ### Updateing State with `setState`
  - when using `setState` react will rerender your entire application
  - and update the UI
  - in react UI is a function of your `state`
  #### A) by passing `setState` a function
  - used when new state depends on the previous state
  ```js
  this.setState((prevState) => ({ 
    count: prevState.count + 1
  }))
  ```
  #### B) by passing `setState` an object
  ```js
  this.setState({
    count: 1
  })
  ```
  
  ## Controlled Components
  - a component which renders a form, where the truth for that form lives inside the component state
  - the input field will show the state of the component, to change what the input field show, you have to change the state of the component
  - supports instant input validation
  - allows to conditionally disable/enable buttons
  - can enforce input formats
  ```jsx
  class NameFrom extends Component {
    state = {email: ''}
    handleChange = (event) => {
      this.setState({email: event.target.value})
    }
    render() {
      return(
        <form>
          <input 
            type="text" 
            value={this.state.email}
            onChange={this.handleChange}
          />
        <form>
      )
    }
  }
  ```
  
'''
linesHighlighted: [
  205
]
isStarred: false
isTrashed: false
