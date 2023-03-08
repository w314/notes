react, angular

# React vs Angular

## Start project

### React
```bash
# create
yarn create vite
# setup git
git init
# start
yarn run dev
```

### Angular
```bash
# create
ng new <project-name>

# git is already set up
# initial commit is made

# start
ng serve
```
<hr />

## Create Basic Page
### 1. Use variable for Title
#### React
```bash
# create component
touch src/components/HomePage.tsx
```
`src/components/HomePage.tsx`
```typescipt
import React from 'react'

export default function HomePage() {
  const title = 'React Home Page'

  return (
    <div>
     {title}
    </div>
  )
}
```

Edit `src/App.tsx`:
```typescript
// import HomePage
import HomePage from './components/HomePage'

// ... code
  return (
    <HomePage></HomePage>
  )
// ... code
```
#### Angular
```bash
# generate component
ng g c components/HomePage
```
Edit `src/app/components/home-page.component.ts`
```typescript
// ...code
export class HomePageComponent implements OnInit {
  // declare title property
  title = 'Angular Home Page'

  // ...code
}
```
`src/app/components/home-page.component.html`:
```html
<!-- use interpolation {{ }}to let information flow  -->
<!-- from component class to the template -->
<h1>{{title}}</h1>
```
`src/app.component.html`:
```html
<app-home-page></app-home-page>
```
### 2. Add counter
#### React
Edit `src/components/HomePage.tsx`
```tsx
// import useState
import { useState } from 'react'

  //...
 
  // use state to manage clickCount
  // useState return an array with two element:
  // count - the current state
  // setCount - the function to use to modify state
  const [count, setCount] = useState(0)

  return (
    // ...
     <h2>Counter</h2>
     {/* use count state to display current count number */}
     <p>{count}</p>
     {/* on click increase current count by one */}
     {/* use the function form of setCount */}
     <button onClick={() => setCount((prevCount) => prevCount + 1)}>+</button>
    //...
```

#### Angular
Edit `src/app/components/home-page.component.html`
```html
<h2>Counter</h2>
<p>{{count}}</p>
<!-- use event (click) binding to connect template -->
<!-- to function declared in component class -->
<button (click)="increaseCount()">+</button>
```
Edit `src/app/components/home-page.component.ts`
```typescript
// declare count property to use in counter
count = 0
// declare function to increase count in counter
increaseCount() {
  this.count = this.count + 1
}
```

<hr />

## Setup Routing
### 1. Setup components for pages
#### React
```bash
touch src/components/HomePage.tsx
touch src/components/Pricing.tsx
```
In each file add code:

(or use `rfc+TAB` if using [ES7+ React/Redux/React-Native snippets](https://marketplace.visualstudio.com/items?itemName=dsznajder.es7-react-js-snippets))
```typescript
import React from 'react'

export default function HomePage() {
  return (
    <div>HomePage</div>
  )
}
```
### 2. Setup Router
#### React
```bash
yarn add react-router-dom
```
Edit `src/main.tsx`
```typescript
// import browser router
import { BrowserRouter } from 'react-router-dom'

// enclose App in <BrowserRouter>
<BrowserRouter>
  <App />
</BrowserRouter>
```
### Angular

If you did **not** include `routing` when setting up the application (if you did, skip this step):
```bash
ng generate module app-routing --flat --module=app
```
- `--flat` puts the file under src/app instead of its own directory
- `--module=app` tells `ng generate` to register it in the imports array of the AppModule (`src/app.module.ts`)

`src/app/app-routing.module.ts`
```typescript
import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';

const routes: Routes = [];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
```

### 2. Create NavBar Component

#### React
```bash
# add components directory
mkdir src/components
# create component
touch src/components/NavBar.tsx
```


#### Angular
```bash
# add components directory
mkdir src/app/components
# generate NavBar component
ng g c components/NavBar
```
`src/app/components/nav-bar/nav-bar.component.ts`:
```typescript

```
- import Router
- add Router as constructor parameter



Edit `src/App.tsx`:
```typescript
// import Routes
import { Routes, Route } from react-router-dom


```
