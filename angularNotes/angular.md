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
> Responsible for handling the view.

To generate component: 
- use `ng g c compName`
- creates 4 files
    - compName.component.ts - CompName Class file
    - compName.component.html - html template
    - compName.component.css - css
    - compName.component.spec.ts - tests


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





Pipes

What is a pipe?

>Pipe is a data transformation.

 

Used for formatting the output.

 

How we create a custom pipe?

`ng g p pipeName`

- will create a class

- annotated with @Pipe

- implements pipeTransform

- has to override transform method

 

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

 

## Directives

What is a directive?

> Instructions for the DOM on how to build the web page.

 

### Custom Directive

 

> Custom Directives are used to change the appearance of the components.

 

Can be used:

- access and manipulate the DOM directly

- resuable functionality

- custom validations for template driven forms

 

To create one:

- use `ng g d myDirective`

- add to `declarations` in `app.module.ts`

- it will create:

`myDirective.directive.ts`

```ts

import { Directive } from '@angular/core'

 

// the @Directive decorator makes the class a directive

@Directive({

    // @Directive decorator has one property: selector

    // with [] it creates an attribute selector

    selector: '[appButton]',

})

 

export class ButtonDirective {

  constructor() {}

}

```

 

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
 

## Forms

 

### Template Driven Forms

 

Advantages

- simplicity

 

Validations are in the template

 

#### Angular form validation

 

Every input has 3 states

- valid / invlaid

- changed / unchanged

- touched / untouched

 

### Reactive Forms

 

Use typescript to do validation

- import ReactiveFormsModule in app.module

- let us use fomrbuilder and validators

 

0. add `ReactiveFormsModule` to `app.module.ts` `imports`

1. create form

`component.ts`

```ts

export class MyClass {

   

    // create form property

    myForm!: FormGroup;

   

    // inject FormBuilder into constructor

    constructor(private formBuilder: FormBuilder ) {}

 

    // initialize form

    onInit() {

        this.myForm = this.formBuilder.group({

            id:['', [Validators.required]],

            name: ['', [Validators.required]],

            age: ['', [Validators.required]]

    })

}

```

 

`component.html`

```ts

 

```

2. add validation

3. use data from form

 

## Routing

 

## Route Parameters

- use :paramName in uri path

 

- use param

`this.route.params.subscribe(para)....?`

 

You cannot pass object as param

 

### Route gurards




 

Page 2 of 2