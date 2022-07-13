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

## Data flow within an application
Ways that data can flow within an application:
- From the component class to the template: `interpolation` -  `{{}}`
- From the template to the component class: `event binding` - `(click)="functionName()"`
- From the parent component to its child component: `input property binding` - `@Input()`
- From child component to its parent component: `output property binding` - `@Output()`

## `Interpolation` and `Input Property Binding`
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
  votes: number;

  // initialize in constractor when using strict mode
  constructor() {
    this.id = 0;
    this.name = '';
    this.diet = '';
    this.votes = 0;
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
      votes: 0,
    }
   }
  
  ngOnInit(): void {
  }
}
```

`zoo-animal.component.html`:
```html
  <h2>{{ animal.name }}<h2>
  <p>Diet: {{ animal.diet }}<p>
  <p>Votes: {{ animal.votes }}</p>
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
      { id: 1, name: 'frog', diet: 'flies', votes: 0},
      {id: 2, name: 'stork', diet: 'frogs', votes: 0}
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

## `Event Binding` and `Output Property Binding`
Add an upvote button and a like button to each animal, let the parent company know if the like button was clicked. 

`zoo-animal.component.html`:
```html
<h2>{{ animal.name }}</h2>
<p><strong>Diet:</strong> {{ animal.diet }}</p>
<p>Votes: {{ votes }}</p>
<!-- 
  Add button for upvotes and like, 
  use event binding to communicate from template to component class
-->
<button (click)="upvote(animal)">Upvote</button>
<button (click)="like(animal)">Like</button>
```

`zoo-animal.component.ts`:
```typescript
// Import Output and EventEmitter for data flow
import { Component, OnInit, Input, Output, EventEmitter } from '@angular/core';
import { Animal } from '../models/Animal'

@Component({
  selector: 'app-zoo-animal',
  templateUrl: './zoo-animal.component.html',
  styleUrls: ['./zoo-animal.component.css']
})
export class ZooAnimalComponent implements OnInit {

  @Input() animal: Animal;
  @Output() likeAnimal: EventEmitter<Animal> = new EventEmitter;

  constructor() {
    this.animal = {id: 0, name: '', diet: '', votes: 0,}
  }

  ngOnInit(): void {
  }

  // create upvote function for event click event
  upvote(animal: Animal): void {
    animal.votes++;
  }

  // create like function, its role is to notify the parent component
  like(animal: Animal): void {
    this.likeAnimal.emit(animal)
  }
}
```

Receive event emitted by child component.
`zoo-component.html`
```html
<h1>{{ title }}</h1>
<!-- 
  bind property likeAnimal decorated by output in child component
  and point it to a function in the parent class
 -->
<app-zoo-animal *ngFor="let animal of animals" [animal]="animal" (likeAnimal)="likeAnimal($event)"></app-zoo-animal>
```
`zoo-component.ts`
```typescript
import { Component, OnInit } from '@angular/core';
import { Animal } from '../models/Animal'

@Component({
  selector: 'app-zoo',
  templateUrl: './zoo.component.html',
  styleUrls: ['./zoo.component.css']
})
export class ZooComponent implements OnInit {
  title: string = 'Animals in the Zoo';
  animals: Animal[] = [];  

  constructor() { }

  ngOnInit(): void {
    this.animals = [
      { id: 1, name: 'frog', diet: 'flies', votes: 0},
      {id: 2, name: 'stork', diet: 'frogs', votes: 0}
    ]    
  }

  // add function to handle event in child componenet
    likeAnimal(animal: Animal): void {
    alert(`You liked ${animal.name}!`)
  }

}
```
