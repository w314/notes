# Angular

## Prerequisites
To use Angular install:
- Node [https://nodejs.org/en/]
- npm by running in terminal: `npm install -g npm`
- angular CLI: `npm install -g @angular/cli 


## Project setup
To create new project run:
```bash
ng new angular_project
```
wasn't asking when i installed a newer version(Answer the questions asked:
- y to stricter type checking
- y to Angular routing
- select stylesheet format)

Start project:
```bash
cd angular_project
ng serve
```
if you want to specify the port use:
`ng serve --port 3000`

## Create component `mycomponent`
- in the root directory of your application run:<br>
`ng generate component mycomponent` or `ng g c mycomponent`
- modify starter code to contain only your content:
- replace contant of `./src/app/app.component.html` whith:
`<app-<componentName>></app-<componentName>>
- it will create a `mycomponent` directory under `src/app`
- it will create 4 files:
    1. `mycomponent.components.css`
    2. `mycomponent.components.html`
    3. `mycomponent.componenets.spec.ts` for tests
    4. `mycomponent.components.ts`

## Display parent component with its children
Creating a Zoo component which will display a list of animals, each list item will be represented by ZooAnimal component.

### 1. Create components
```bash
ng g c Zoo
ng g c ZooAnimal
```
### 2. Create model Animal data type
```bash
mkdir src/app/models
touch src/app/models/Animal.ts
```
With the content:
```typescript
export class Animal {
  id: number;
  name: string;
  diet: string;

  // initialize in constractor when using strict mode
  constructor() {
    this.id = 0;
    this.name = '';
    this.diet = '';
  }
}
```

### Set up `zoo-animal` Component
> use the `@Input` decorator to get data from parent component

`zoo-animal.component.ts`:

```typescript
// import Input to get data from parent component
import { Component, OnInit, Input } from '@angular/core';
// import Animal model
import { Animal } from '../models/Animal'

@Component({
  selector: 'app-zoo-animal',
  templateUrl: './zoo-animal.component.html',
  styleUrls: ['./zoo-animal.component.css']
})
export class ZooAnimalComponent implements OnInit {

  // create variable for animal
  // use @Input decorator to indicate data comes from parent component
  @Input() animal: Animal 

  // intitalize animal in constructor when using strict type cheking
  constructor() {
    this.animal = {
      id: 0,
      name: '',
      diet: '',
    }
   }
  
  ngOnInit(): void {
  }
}
```

`zoo-animal.component.html`:
```html
  <h2>{{ animal.name }}<h2>
  <p>{{ animal.diet }}<p>
```

### Setup `zoo` component

```typescript
import { Component, OnInit } from '@angular/core';
// import Animal data type
import { Animal } from '../models/Animal'

@Component({
  selector: 'app-zoo',
  templateUrl: './zoo.component.html',
  styleUrls: ['./zoo.component.css']
})
export class ZooComponent implements OnInit {
  // add animals property
  title: string = 'Animal is the Zoo';
  animals: Animal[] = [];
  
  constructor() { }

  // initialize animals property
  ngOnInit(): void {
    this.animals = [
      { id: 1, name: 'frog', diet: 'flies'}, {id: 2, name: 'stork', diet: 'frogs'}
    ]
  }
}
```
`zoo.component.html`
```html
  <h1>{{ title }}</h1>
  <!-- set up rendering child components passing data along -->
  <app-zoo-animal *ngFor="let animal of animals" [animal]="animal"></app-zoo-animal>
```

### Include Zoo component when rendering App
`app.component.html`
```html
<app-zoo></app-zoo>
```