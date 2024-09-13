How to change tag selector to attribute selector?
# Angular

Singe Responsibility Principle
- components handle reusable view
- services handle reusable funcionality

## Create & Start Angular App
```bash
ng init appName
# say yes for routing
cd appName/src/app
ng serve --open
```

## Components
> Controls a patch of the screen (view).
- basic building blocks of the angular application
- components are defined by a typescript class marked by the `@Component` decorator
- components are custom HTML tags, tagname = selector

### Component Structure
- `myComp.comonent.ts`  - business logic
- `myComp.component.html` - view that gets rendered
- `myComp.component.css`  - custom styling
- `myComp.component.spec.ts` - for test cases

### Basic Component
`appComponent.component.ts`
```ts
// need the import of Component
import { Component } from '@angular/core';
// marked by @Component decorator
@Component({
  // selector name is used to render the component like: <app-root></app-root>
  selector: 'app-root',
  // the view to be rendered  
  templateUrl: './app.component.html',
  // array of stylesheets to be used
  styleUrls: ['./app.component.css']
})

// class is exported to be used in other components
export class AppComponent {
  // a class property is defined
  title:string = 'MyApp';
}
```

`AppComponent.component.html`
```html
<!-- interpolation with {{ }} is used to access class property -->
<p>The component {{ title }} is working!</p>
```

## Modules
> Modules are the mechanism to group a set of components, directive, pipes, services that are related to a particular application.
- All components are grouped together under the same module, the root module: AppModule.
- Using modules we can group certain components together and load only the ones that we need.
- Every angular applications will have at least one module.


`app.module.ts`
```ts
// BrowserModule class is need to run the application in a browser
import { BrowserModule } from '@angular/platform-browser';
// NgModule class defines metadata of the module
import { NgModule } from '@angular/core';
// AppRoutingModule for routing
import { AppRoutingModule } from './app-routing.module';
// import the AppComponent class (created automatically with ng new command)
import { AppComponent } from './app.component';

// module is decorated with @NgModule
@NgModule({
  // contains all user defined component, directive, pipe classes of the module
  declarations: [ AppComponent ],
  // all outside modules used
  imports: [ BrowserModule, AppRoutingModule ],
  // service class of the module
  providers: [],
  // the root component to load
  bootstrap: [AppComponent]
})

export class AppModule { }
```

## How Angular App Works

1. Module is defined in `app.module.ts`
2. Root component to load is defined
    - in `app.module.ts`
    - in the `Bootstrap` declaration
3. Bootstrapping root module
`src/main.ts`
```ts
// compiles application based on browser platform
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
// root module to bootstrap
import { AppModule } from './app/app.module';

platformBrowserDynamic().bootstrapModule(AppModule)
  .catch(err => console.error(err));
```
4. Load root component in the HTML page
`src/index.html`
```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title>MyApp</title>
  <base href="/">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="icon" type="image/x-icon" href="favicon.ico">
</head>
<body>
  <!-- loads root module -->
  <app-root></app-root>
</body>
</html>
```

## Templates
>Template is an HTML file that represents the view of the component.

ELemenst of a template:
- html
- interpolation
- template expressions
- template statements

### Interpolation
> Used to access the properties and methods of the component class inside the view.

```html
<!-- access properties -->
<p>Hi {{ name }} !</p>

<!-- invoke methods -->
<p>Your name starts with {{ name.substr(0, 2)}}.</p>

<!-- to avoid errors in case property is null use ? -->
<p>{{ name?.substr(0, 2)}}</p>
```

### Template Expressions
We can use `{{}}` to perform general expressions.

```html
<p>{{ 'hello'.toUpperCase() }}</p>

<p>{{ num % 2 == 0 ? 'Even Number' : 'Odd Number' }}</p>
```
You cannot use: `new`, `++`, `--`, `+=`, `-=`

### Template Statements
> Template statements respond to user-defined events

```html
<button (click)="myFunction()">Call My Function</button>

<!-- can be an expression -->
<form (ngSubmit)="submitted=true">
```
- also called event binding
- event has to be enclosed in `()`
- function has to called with `()`


### Template Variables

Template reference variables most often a reference to a DOM element in the template.

They can also refer to:
- angular components
- directives
- web components

```html
<!-- use #variableName -->
<input #name type="text">
<button (click)="showName(name.value)">Show Name</button>
```
- it can also be used to change that element's value


### Data Binding



- put selector name in square brackets `[]`

 

Data Binding

 

how do we bind data that we want to display?

- using interpolation `{{}}`

 

how do we bind data form our ts to our html for porperties or formatting

- using porperty binding with `[property-name]="tsVariable"`

 

how do we bind from html to typescript

- event binding wiht `(eventName)="expression"`

- expression usually is a function call `myFunction()`

 

how to do two way binding

-  `[(ngModel)]="tsVariable"`

- need modules `FormModules` in `ngModule`





## Pipes
> Pipes are used to format data before displaying it.

`{{ expression | pipe }}`


### Built In Pipes

- uppercase
- lowercase
- titleCase
- json
- currency
- date
- slice
- decimal
- percent


### Custome Pipes

To create a customer pipe:
```bash
ng generate pipe myPipe
# OR
ng g p myPipe
```

The command will create a class:

`my-pipe.pipe.ts`
```ts
import { Pipe, PipeTransform } from '@angular/core';

// class is decorated with @Pipe decorator
@Pipe
({
  name: 'myPipe'
})

// class inherits PipeTransform interface
export class MyPipe implements PipeTransform
{

    // has to override transform method
    transform(value: any, ...arg:any[]):any {}
}
```
- transform method has two parameters:
    - value to transform
    - any number of parameters

Example:
```ts
@Pipe ({ name: 'salutation'})

export class Salutation implements PipeTransform {
    
    transform(name: string, gender: string): string {
        if(gender == "M") {
            return `Mr ${name}`
        } else if(gender == "F") {
            return `Ms ${name}`
        } else {
            return name;
        }
    }
}
```




How do we nest component?

 

How do we render child component, how do we nest the component?

- putting the tag inside of another component

 

what does the Input decorator do in the child component:

> creates a property of the child component tag

 

What do we do with the property of the child component tag?

- we do a property binding on the parent html

 

How to we send information from child to parent

- use @Outptu

 

What od we put the output decorator on?

- we annotate an event emitter

 

How do we casue the event to happen

- use the emit() function on the emitter

- `emitter.emit(emittedValue)`

 

Next step

-bind to that event in the parent

 

 

## Passing Data Between Components

 

### Parent -> Child

 

#### Parent

`parent.component.ts`

```ts

export class Parent {

    genre = "fiction";

}

```

`parent.component.html`

```html

<app-child [genre]="genre"></app-child>

```

 

#### Child

- use `@Input()`

- specifies that the data is coming form container component

- creates a property

- make property public for binding from Angular perspective

- property can receive input from any other component or directive

 

`child.component.ts`

```ts

import { Component, Input } from `@angular/core`

 

export class Child {

 

    @Input()

    genre: string = "";

}

```

 

### Child -> Parent

 

#### Child Sending Data

Child must use event to pass data to parent

 

`child.component.ts`

```ts

export class Child {

 

    // set up event emitter

    @Output()

    myEvent: EventEmitter<number> = new EvenEmitter<number>();

 

    // use event emitter to pass data to parent component

    sendDataToParent() {

        this.myEvent.emit(29);

    }

 

}

```

 

#### Parent Receiving Data

 

`parent.component.ts`

```ts

 

```

## Component LifyCycle

> Compoment has a life cycle managed by Angular.

 

`component.ts`

```ts

// class has to implement onInit

export class MyComponent implement onInit, onDestroy {

 

// override lifcycle hooks

ngOnInit() {}

 

ngOnDestroy() {}

}

```

 

### onInit

- called after `constructor()`

- constractor should be empty, initalizaiton happens in onInit




## Services
> A service is a class that contains some functionality that can be reused accross the application.
- singleton object
- wired using dependency injection
- there are built-in services
- can build cutom ones
- there is no decorator to indicate it is a service class

### How to Create a Service
- create a service
- inject the service into the component
- provide the servicde in module class

#### 1. Create / Define a  Service
 ```bash
 ng generate service serviceName
#  OR
ng g s serviceName
```

Service file: `number.service.ts`
```ts
export class NumberService {

    constructor() {}
    
    // add functionality of providing a number
    getNumber(): number {
        return 2;
    }
}
```

#### 2. Inject Service into Component
`number.component.ts`
```ts
import { Component } from '@angular/core';
import { NumberService } from './number.service'

@Component({
    selector: 'app-number'
})

export class NumberComponent implements onInit {

    // variable that will get value from service
    number!: number;

    // service instance is passed in Component's constructor
    constructor(private numberService: NumberService) {}

    // invoke services' method to populat number variable 
    // when component is intitialized
    ngOnInit() {
        this.number = this.numberService.getNumber();
    }
}
```

#### 3. Provide Service

`app.module.ts`
```ts
@NgModule({
    providers: [
        // provide & useClass can use different names
        { provide: NumberService, useClass: NumberService }
    ]
    //  OR simply:
    providers:[
        NumberService
    ]
})
```

### Dependency Injection

- dependecy injection means angular is handling / maintaining the service for you
- HTTP requests are asynchronous
- HTTP methods will automatically convert received json to desired type
- `http.get()` by default returns and `observable`

### `Observables`
> A collection that arrives over time.

- produces data that the subscriber can subcribe to and use
- `.subscribe()` method is used to subscribe
- facilitates asynchronous communications
- handled by a third party library `RxJs`

Observables over Promises as:
- Promise emits a single value vs the observables's streams
- observables can be cancelled, Promises cannot
- observables suppeort functional operators like: map, filter, reduce, etc



### `HttpClientModule`
> Used to communicate with backend services to fetch or persist data.

#### 1. Add to imports in module class

`app.module.ts`
```ts
import { HttpClientModule } from '@angular/common/http';

@NgModule({
    imports: [BrowserModule, HttpClientModule]
})
```

#### 2. Make HTTP calls in service class

`myService.service.ts`:

Imports needed:
```ts
import { Injectable  } from '@angular/core';
import { HttpClient } from '@angular/common/http'
import { Observable } from 'rxjs'
// type definition for Book Type
import { Book } from './book'
```

Inject HttpClient into Service
```ts
import { Injectable }
// user @Injectable decorator that the service
// has its own depencenty injections
@Injectable({
    providedIn: 'root'
})
// OR 
// if you have added HttpClientModule to imports as above
@Injectable()
export class MyService {

    // inject HttpClient into constructor
    constructor(privet http: HttpClient) {};
}
```

Make HTTP calls
```ts
@Injectable()
export class MyService {

    // variable to store URL
    private booksUrl = './assets.books.json';
    private addBookUrl = './localhost/books';

    constructor(private http: HttpClient) {}

    // get Data function makes HTTP call
    // returns an observable with an array of Books 
    getBooks(): Observable<Book[]> {
        // get method will automatically convert received json
        // to array of Books
        return this.http.get<Book[]>(
            this.booksUrl
        );
    }

    // post mehtod will send a book to be added
    // return added book from server
    addBook(book: Book): Observable<Book> {
        return this.http.post<Book>(
            this.addBookUrl,
            book
        )
    }
}
```

#### 3. Use Service in Component

`book.component.ts`
```ts
export class BookComponent implements OnInit {

    books!: Book[];
    // to store errosmessge received from HTTP call
    errorMessage = "";

    constructor(private bookService: BookService) {};

    // function to get books from service
    getBooks() {
        // subscribe to the observable provided by 
        // bookService's getBooks() method
        this.bookService.getBooks().subscribe(
            // first argument handles success
            books => this.books = books, 
            // second arugment handles failure
            error => this.errorMessage = <any> error
            // third argument wold handel closure of subscription
            // () => {}
        );
    }

    // get books at compnent initialization
    ngOnInit() {
        this.getBooks();
    }
}
```

Display books in: `book.component.html`
```html
<ul>
    <li *ngFor="let book of books">
        {{ book.name }}
</ul>
<!-- display error message if needed -->
<div *ngIf="erroMessage">{{ errorMessage }}</div>
```

 

## Template Driven Forms

 

Advantages

- simplicity

 

Validations are in the template

 

#### Angular form validation

 

Every input has 3 states

- valid / invlaid

- changed / unchanged

- touched / untouched

 

## Reactive Forms / Model Driven Forms
> We create control objects in a component class and bind to HTML form elements.

- we can push and fetch data to and form the HTML form
- component can observe changes in form control state and react to it
- value and validity updates are synchronous and under our control
- we use the `FormBuilder Class` to create reactive forms

Advantages:
- we can unit test validation logic
- we can listen to form changes or events easily

### How to Create Reactive Form

#### 1. Add `ReactiveFormsModule` to `imports`

`app.module.ts`
```ts
@NgModule({
    imports: [
        ReactiveFormsModule
    ]
})
```

#### 2. Create From in Component

`myComponent.component.ts`
```ts
export class MyComponent implements OnInit{

    // create formGroup variable
    userForm!: FormGroup;
    sumbitted = false;

    // inject formBuilder instance
    constructor(private formBuilder: FormBuilder) {}

    ngOnInit() {
        // create formGroup and assign to variable
        // use group() method of formBuilder object
        // takes an object key -value pairs
        // keys are the FormControl name
        // values are the FormControl definitions
        this.userForm = this.formBuilder.group({
            // first parameter of the FormControl definition
            // is the default value
            // second is an array of Validators
            name: ['', [Validators.required]],
            address: this.formBuilder.group({
                city: [],
                zip: []
            })

        })
    }
}
```

### 3. Bind formGroup to HTML form elements

`my-component.component.html`
```html
<!-- bind form to formGroup -->
<!-- add event binding for submission--> 
<form [formGroup]="userFrom">
    <div>
        <label>Name</label>
        <!-- bind HTML form element to formControl -->
        <input type="text" formControlName="firstName">
        <!-- display error message for invalid control -->
        <p *ngIf="registerForm.controls['firstName'].errors">
            This field is required!</p>
    </div>
    <div>
      <fieldset formGroupName="address">
          <label>City</label>
          <input type="text" class="form-control" formControlName="city">
        <label>Zip</label>
        <input type="text" class="form-control" formControlName="zip">
      </fieldset>
    </div>
    <button type="submit">Submit</button>
</form>
```

#### Send form input to server

`myComp.component.html`
```html
<!-- bind submit event to calling sendData() function -->
<form [formGroup]="myForm" (ngSubmit)="sendData()">
    <button type=submit></button>
</form>
<!-- give feedback about success of submission -->
<p *ngIf="successMessage">{{successMessage}}></p>
<p *ngIf="errorMessage">{{errorMessage}}></p>
```
`myComp.component.ts`
```ts
export class MyComp {
    myForm!: FormGroup;
    constructor(private myService: MyService)
    successMessage = "";
    errorMessage = "";
    
    // sendData function will call service's sendData() functon
    // and will send form values
    // and subscribes to its response
    sendData() {
        this.myService.sendData(this.myForm.value).subscribe(
            (responseData) => this.sucessMessage = "OK"
            (error) => this.errorMessage = "AJAJ"
        );
    }
}

### Validators

You add validator when creating the FormGroup in the component.

#### `updateOn`

- `updateOn` determines when Angular runs the validation process.
- speeds up the applications when not running them at every keystroke

Possible Values:
- `change` 
    - at every keystroke
    - default
- `blur`
    - when the form loses focus
- `sumbit`
    - when the form is submitted

`myComp.component.ts`:
```ts
    ngOnInit() {
        this.myForm = this.formBuilder.group({
            name: ['', {
                updateOn: 'blur',
                validators: [Validators.required]
            }]
        })
```

### Custem Validators

`myComp.component.ts`
```ts
...
export class RegistrationFormComponent implements OnInit {
//  ...
  ngOnInit() {
    this.registerForm = this.formBuilder.group({
      name: ['', [
        Validators.required,
        validateName
      ]],
    });
  }
}

// take formControl as argument
function validateName(c: FormControl) {

    return c.value == "Bob" 
    // if value is valid we return null
    ? null
    // otherwise return an object with a key and value
    // value can be an object
    : {
        nameError: { message: "Name should be Bob"}
    };
}
```

### Displey error messages in HTML Form

`myComp.comonent.html`
```html
<p *ngIf="myForm.controls['name'].errors!['nameError']">
    {{ myForm.controls['name'].errors!['nameError'].message }}
</p>
```
function validateName(n: string)


```ts
export class MyComp implements OnInit {

    myForm!: FormGroup

    constructor(private formBuilder: FormBuilder) {}

    ngOnInit() {
        this.myForm = this.formBuilder.group({
            name: ['', [

            ]]
        })
    }
} 
```