# Angular Templates
>Template is an HTML file that represents the view of the component.

Ways to attach templat to a component
1. Inline Templete
```js
@Component {
    template: `<h1>hi</h1>`
}
```
2. External Template
```js
@Component {
    templateUrl: './app.component.html'
}
```

ELemenst of a template:
- html
- interpolation
- template expressions
- template statements
- template variables

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
It can also be used to change that element's value.

