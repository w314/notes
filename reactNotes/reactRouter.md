react, router, routes

# React Router
```bash
yarn add react-router-dom
```
`main.tsx`
```tsx
import { BrowserRouter } from 'react-router-dom'
// ...
<BrowserRouter>
    <App />
</BrowserRouter>
//...
```

`src/App.tsx`
```tsx
import { Routes, Route, Navigate } from 'react-router-dom'

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

export default App
```
OLD:
