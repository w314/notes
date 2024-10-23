angular, data transfer

# Data Binding in Angular
> Data binding means communication between the typescript class code (business logic) and the template (what the user sees on the screen)

## Types of Data Binding
- one-way binding
    - output data to template
        - string interpolation `{{dataFromClassCode}}`
        - property binding `([propertyName]="data")`
    - react to user events
        - event binding `((event)="expression")`
- two-way binding
    - `[(ngModel)]="data"`

## Interpolation

- one way data binding
- from template -> view

`app.component.ts`
```ts
export class AppComponent {
    name = 'bob';
}
```
`app.component.html`
```html
<p>Hi {{name}}!</p>
```

