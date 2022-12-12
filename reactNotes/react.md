# react

## Setup project

### 1. Create react project with typescript:

A) using `vite`
```bash
npm create vite
cd yourApp
npm install
npm run dev
```
- the `app name` will be also the name of the folder created for the app
- select `react` as framework
- select `typescript` as variant


B) also possible to create with `create-react-app`
```bash
npx create-react-app myApp --template typescript
```

It comes with npm warinings:


[Handlig vulnerabilities that are comming up](https://github.com/facebook/create-react-app/issues/11174)
- move `react-srcipts` to `dev-dependencies`
- run `npm audit --omit=dev`

## Routing

Install `react router`

```bash
npm i react-router-dom
```

Edit `src/main.tsx`:
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

### 2. Add `esLint` and `Prettier`
```bash
npm i --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
npm i --save-dev prettier eslint-config-prettier eslint-plugin-prettier
```

Add configuration files:
```bash
echo '{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "plugins": [
    "@typescript-eslint",
    "prettier"
  ],
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/eslint-recommended",
    "plugin:@typescript-eslint/recommended",
    "prettier"
  ],
  "rules": {
    "no-console": "off",
    "prettier/prettier": 2 // Means error
  }
}
' > .eslintrc
echo '{
  "semi": true,
  "singleQuote": true
}' > .prettierrc

```

Add `package.json` scripts:
```bash
"scripts": {
    "prettier": "prettier --config .prettierrc \"src/**/*{js,ts,tsx}\" --write",
    "eslint": "eslint \"src/**/*.{js,ts, tsx}\"",
    "lint": "npm run prettier && npm run eslint"
}
```


OLD:

```bash
mkdir src/components
touch src/components/Navbar.js
```


