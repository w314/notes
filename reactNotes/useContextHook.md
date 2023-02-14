react, useContext, hooks

# React useContext() hook
## Why
- passing data as props to components may mean that a lot of components have to deal with props they themselves don't need. (If useState is in App.tsx and the component that needs the data is several component layer down for example.)
- As app needs to know the props of the child component to call it, so you cannot change the implementation of the child component without changing App.tsx

