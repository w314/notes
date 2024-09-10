angular, router

# Angular Router
> Routing is a navigaton between multiple views in a single page
- allows to express some aspects of application state in the URL
- angular cli creates `app-routing.module.ts` file when chosing to include routing at app creation

## 1. Set Up Routes

Define routes in `app-routing.module.ts`:
```ts
// set up routes
const routes: Routes = [
    // pathMatch:"full" matches exact path only
    {path: "list", component: ListComponent, pathMatch: "full"},
    // :id lets us pass path parameters
    {path: "item/:id", component: ItemComponent, pathMatch: "full"},
    // path ** matches any path and redirects to list 
    {path: "**", redirectTo: "list"}
];
```

## 2. Set Up Navigation
Activate routing in `app.component.html`
```html
<h1>My App</h1>
<nav>
    <!-- using routerLink instead of href will not reload the page -->
    <!-- routerLink navigates to new url and component with render -->
    <!-- at the place detemined by router-outlet -->
  <a [routerLink]="['list']">List</a>
  <a [routerLink]='["item"]'>Item 3</a>
</nav>

<!-- router oulet determines where the ouput of the component-->
<!-- associated with the path will be displayed -->
<router-outlet></router-outlet>
```

### 3. Pass parameter with routerLink

```html
<ul *ngFor="let book of books">
    <!-- pass parameter in routerLink array -->
     <!-- without the / the link address would add item after current URL like list/item -->
    <li><a [routerLink]="['/item', book.id]">{{ book.name }}</a></li>
</ul>
```

### 4. Navigate programatically

```ts
export class MyComponent  {

    // injedt router to constructor
    constructor(private router: Router) {}

    goToBook(id: number) {
        this.router.navigate(['/item', id])
    }
}
```

### 5. Retrieve Parameter form URL

```ts
export class MyComponent {

    id: number;

    // inject ACTIVATED Route
    constructor(private route: ActivatedRoute) {  }

    ngOnInit() {
        this.route.params.subscribe(param => this.id = param['id']);
        
    }
}
```



### 4. Retrive parameter from URL



## Route Parameters

- use :paramName in uri path

 

- use param

`this.route.params.subscribe(para)....?`

 

You cannot pass object as param

 

### Route gurards