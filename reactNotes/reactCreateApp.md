react

# Create a React App
## Create Starter App
```bash
#  if using with TypeScript
npx create-react-app <app-name> --template typescrpipt

# if you do not want a git repository use
npx create-react-app <app-name> --template typescrpipt --no-git

# cd int app directory
# start react app
npm start
```

## Bootstrap
- bootstrap and [react-bootstrap](https://react-bootstrap.github.io/) help with easy styling

In `App.tsx`:
```tsx
// import bootstrap
import 'bootstrap/dist/css/bootstrap.min.css';
```

Import needed elements in  Components:
```tsx
import { Modal, Container } from "react-bootstap";
```


## React Router

# React Router

Add react router to project
```bash
npm add react-router-dom
```

Wrap `<App />` in `<BrowserRouter>`.
`index.tsx`
```tsx
import { BrowserRouter } from 'react-router-dom'
// ...
<BrowserRouter>
    <App />
</BrowserRouter>
//...
```

Setup Routes
`src/App.tsx`
```tsx
import { Routes, Route } from 'react-router-dom'

function App(){
    return (
      <Routes>
        <Route path='/' element={<h1>STORE</h1>} />
        <Route path='/cart' element={<h1>CART</h1>} />
                <Routes>
        <Route path='/products' element={<h1>Hi</h1>}/>
        <Route path='/new' element={<h1>NEW</h1>} />
        {/* routes can be nested */}
        <Route path='/:id'>
            {/* index: the path of parent route */}
            <Route index element={<h1>Show</h1>} />
            <Route path='edit' element={<h1>Edit</h1>} />
        </Route>
        <Route path='*' element={<Navigate to='/' />} />
      </Routes>
        {/* redirecting any non-existent path to home page */}
        <Route path='*' element={<Navigate to='/' />} />
      </Routes>
    )
}
```
