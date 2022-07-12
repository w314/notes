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
    4. `mycomponent.components.ts`:
    ```bash
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-recipe',
  templateUrl: './recipe.component.html',
  styleUrls: ['./recipe.component.css']
})
export class RecipeComponent implements OnInit {

  name: string = 'Lemonade'
  ingredients: string [] = ['lemon', 'water', 'sugar']


  constructor() { }

  ngOnInit(): void {
  }

  getIngredients() {
    let output: string = ''
    console.log(this.ingredients)
    this.ingredients.forEach(ingredient => output += `<li>${ingredient}</li>`)
    return output;
  }

}

    ```


## Use variables in component
- in your `mycomponent.components.ts` file you can set up variables, function t use in your `mycomponent.component.html` file by including them within `{{ }}`


    
        
