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

- y to Angular routing
- select stylesheet format

Start project:

```bash
cd angular_project
ng serve
```

if you want to specify the port use:
`ng serve --port 3000`

## Angular Components

- angular is based on components
- each component is a typescript class that has all the logic your component needs
- each component typescript class has a `@Component()` decorator to specify metadata about the class (HTML template, styles)
- name of the file is `YourComponentName.component.ts`
- the default component created is called `App`:

```typescript
import { Component } from "@angular/core";

// use @Component() decorator for metadata for your class
@Component({
  // you use selector just as regular HTML tags to include
  // the component within other templates
  selector: "app-root",
  // html template url, it declares how the component
  // renders
  templateUrl: "./app.component.html",
  // styles url
  styleUrls: ["./app.component.css"],
})

// name of the class is same as based on the name of the component
export class AppComponent {
  // your component logic goes here
  title = "ang";
}
```

- browser will render template provdied in `app.component.html`:

```html

```

- using styles provided in `app.component.css`
- `@Component()` decorator can be used to provide inline HTML or the styles directly

```typescript
@Component(
  selector: 'app-item',
  // use backticks for HTML template string
  templateUrl:`<h1>Hi!</h1>`,
  // provide style in decorator
  styles: ['h1 {color: red;}']

)
```

### create component `ItemComponent`

- in the root directory of your application run:<br>
  `ng generate component item` or `ng g c item` for short
- it will create a `item` directory under `src/app`
- it will create 4 files within the `item` direcory:
  1. item.component.css
  2. item.component.html
  3. item.componenet.spec.ts
  4. item.component.ts

## Data flow within an application

Ways that data can flow within an application:

- From the component class to the template: `interpolation` - `{{}}`
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
    this.name = "";
    this.diet = "";
    this.votes = 0;
  }
}
```

### Set up `zoo-animal` Component

> use the `@Input` decorator to get data from parent component

`zoo-animal.component.ts`:

```typescript
// import Input to get data from parent component
import { Component, OnInit, Input } from "@angular/core";
// import Animal model
import { Animal } from "../models/Animal";

@Component({
  selector: "app-zoo-animal",
  templateUrl: "./zoo-animal.component.html",
  styleUrls: ["./zoo-animal.component.css"],
})
export class ZooAnimalComponent implements OnInit {
  // create variable for animal
  // use @Input decorator to indicate data comes from parent component
  @Input() animal: Animal;

  // intitalize animal in constructor when using strict type cheking
  constructor() {
    this.animal = {
      id: 0,
      name: "",
      diet: "",
      votes: 0,
    };
  }

  ngOnInit(): void {}
}
```

`zoo-animal.component.html`:

```html
<h2>
  {{ animal.name }}
  <h2>
    <p>Diet: {{ animal.diet }}</p>
    <p></p>
    <p>Votes: {{ animal.votes }}</p>
  </h2>
</h2>
```

### Setup `zoo` component

```typescript
import { Component, OnInit } from "@angular/core";
// import Animal data type
import { Animal } from "../models/Animal";

@Component({
  selector: "app-zoo",
  templateUrl: "./zoo.component.html",
  styleUrls: ["./zoo.component.css"],
})
export class ZooComponent implements OnInit {
  // add animals property
  title: string = "Animal is the Zoo";
  animals: Animal[] = [];

  constructor() {}

  // initialize animals property
  ngOnInit(): void {
    this.animals = [
      { id: 1, name: "frog", diet: "flies", votes: 0 },
      { id: 2, name: "stork", diet: "frogs", votes: 0 },
    ];
  }
}
```

`zoo.component.html`

```html
<h1>{{ title }}</h1>
<!-- set up rendering child components passing data along -->
<app-zoo-animal
  *ngFor="let animal of animals"
  [animal]="animal"
></app-zoo-animal>
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
import { Component, OnInit, Input, Output, EventEmitter } from "@angular/core";
import { Animal } from "../models/Animal";

@Component({
  selector: "app-zoo-animal",
  templateUrl: "./zoo-animal.component.html",
  styleUrls: ["./zoo-animal.component.css"],
})
export class ZooAnimalComponent implements OnInit {
  @Input() animal: Animal;
  @Output() likeAnimal: EventEmitter<Animal> = new EventEmitter();

  constructor() {
    this.animal = { id: 0, name: "", diet: "", votes: 0 };
  }

  ngOnInit(): void {}

  // create upvote function for event click event
  upvote(animal: Animal): void {
    animal.votes++;
  }

  // create like function, its role is to notify the parent component
  like(animal: Animal): void {
    this.likeAnimal.emit(animal);
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
<app-zoo-animal
  *ngFor="let animal of animals"
  [animal]="animal"
  (likeAnimal)="likeAnimal($event)"
></app-zoo-animal>
```

`zoo-component.ts`

```typescript
import { Component, OnInit } from "@angular/core";
import { Animal } from "../models/Animal";

@Component({
  selector: "app-zoo",
  templateUrl: "./zoo.component.html",
  styleUrls: ["./zoo.component.css"],
})
export class ZooComponent implements OnInit {
  title: string = "Animals in the Zoo";
  animals: Animal[] = [];

  constructor() {}

  ngOnInit(): void {
    this.animals = [
      { id: 1, name: "frog", diet: "flies", votes: 0 },
      { id: 2, name: "stork", diet: "frogs", votes: 0 },
    ];
  }

  // add function to handle event in child componenet
  likeAnimal(animal: Animal): void {
    alert(`You liked ${animal.name}!`);
  }
}
```

## Navigation

Creating a new component About, and setup a router and navbar.

### 1. Generate `About` Component

```bash
ng g c About
```

### 2. Configure router

#### 2.a [Add the `AppRoutingModule`](https://angular.io/tutorial/toh-pt5#add-the-approutingmodule) if you dont have one already

In Angular, the best practice is to load and configure the router in a separate, top-level module. The router is dedicated to routing and imported by the root `AppModule`.

By convention, the module class name is `AppRoutingModule` and it belongs in the `app-routing.module.ts` in the `src/app` directory.

Run ng generate to create the application routing module.

```bash
ng generate module app-routing --flat --module=app
```

`--flat` Puts the file in src/app instead of its own directory.<br>
`--module=app` Tells ng generate to register it in the imports array of the AppModule.

#### 2.b Configure Router

Edit `app-routing.module.ts` to include:

```typescript
import { NgModule } from "@angular/core";
import { Routes, RouterModule } from "@angular/router";
import { ZooComponent } from "./zoo/zoo.component";
import { AboutComponent } from "./about/about.component";

const routes: Routes = [
  { path: "", component: ZooComponent },
  { path: "About", component: AboutComponent },
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule],
})
export class AppRoutingModule {}
```

### 3. Create NavBar Component

```bash
ng g c NavBar
```

Modify `nav-bar-component.html` to:

```html
<nav>
  <ul>
    <!-- 
      Using routerLink instead of href allows navigation without reloading the pages.
      Make not of the using / for root.
    -->
    <li><a routerLink="/">Zoo</a></li>
    <li><a routerLink="/About">About</a></li>
  </ul>
</nav>
```

### 4. Add Navbar and Router to home page

Modify `app.component.html` to:

```html
<app-nav-bar></app-nav-bar> <router-outlet></router-outlet>
```

## Setting up services

Components supposed to only deal with UI, the data we used above should be provided by services.

### Create service the get animal data

- in on step we create `services` directory as weel as the `animal` service

```bash
ng g s services/animal
```

- in `animal.service.ts` add a `getAnimals()` function to get the data

```typescript
import { Injectable } from "@angular/core";

@Injectable({
  providedIn: "root",
})
export class AnimalService {
  constructor() {}

  // add function to get data
  getAnimals() {
    return [
      { id: 1, name: "frog", diet: "flies", votes: 0 },
      { id: 2, name: "stork", diet: "frogs", votes: 0 },
    ];
  }
}
```

### Add service to zoo component

- remove hard coded data from zoo component
- import AnimalService
- set is as a parameter of the constructor
- use the service to get the data

```typescript
import { Component, OnInit } from "@angular/core";
import { Animal } from "../models/Animal";
// import AnimalService to provide animal data
import { AnimalService } from "../services/animal.service";

@Component({
  selector: "app-zoo",
  templateUrl: "./zoo.component.html",
  styleUrls: ["./zoo.component.css"],
})
export class ZooComponent implements OnInit {
  title: string = "Animals in the Zoo";
  animals: Animal[] = [];

  // set AnimalService as a parameter of the  constructor
  constructor(private animalService: AnimalService) {}

  ngOnInit(): void {
    // get data from AnimalService
    this.animals = this.animalService.getAnimals();
  }
  likeAnimal(animal: Animal): void {
    alert(`You liked ${animal.name}!`);
  }
}
```

l

### Add a service to handle data sharing among unrelated components

Ideal service like that could be a bookmark manager, in this case the service will handle a favourite animal list.

- create service for favourite animals

```bash
ng g s services/favouriteAnimals
```

- edit `favourite-animals.service.ts`:

```typescript
import { Injectable } from "@angular/core";
// import Animal model
import { Animal } from "../models/Animal";

@Injectable({
  providedIn: "root",
})
export class FavouriteAnimalsService {
  favouriteAnimals: Animal[] = [];
  constructor() {}

  // function to provide list of favourite animals
  getFavouriteAnimals() {
    return this.favouriteAnimals;
  }

  // function to add animal to list of favourite animals
  addFavouriteAnimal(animal: Animal) {
    this.favouriteAnimals.push(animal);
    return this.favouriteAnimals;
  }

  // function to clear favourite animals list
  clearFavouriteAnimalList() {
    this.favouriteAnimals = [];
    return this.favouriteAnimals;
  }
}
```

- add `Add to Favourite` button to `app-zoo-animal.component.html`

```html
<!--   Add button to add animal to favourite animal list -->
<button (click)="favourite(animal)">Add to Favourite</button>
```

- communicate click of `Add to Favourite Animals` button to `FavouriteAnimalsService` in `app-zoo-animal.component.ts`:

```typescript
  /* ..  */
  // create event emitter to communicate clik of
  // Add to Favourite Animals button to parent component
  @Output() addToFavourite: EventEmitter<Animal> = new EventEmitter;
  /* ..  */
  // create favourite function that is called when
  // Add To Favourite Animals button is clicked
  favourite(animal: Animal): void {
    // use emitter to emit click event
    this.addToFavourite.emit(animal)
  }
```

- look for `addToFavourite` emitter in `zoo-app.component.ts`
