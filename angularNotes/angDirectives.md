angular, directive
# Angular Directives
> Instructions for the compiler about how to build DOM elements.

## Types of Directives
- Components
  - directives with a template (view)
  - `@Component` = @Directive with template
- Structural Directives
  - `*directive-name = expression`
  - changes the DOM structure by
    - adding elements
    - removing elements
  - types:
    - `*ngIf`
    - `*nfFor`
    - `*ngSwitch` 
- Attributes Directives
  - used to modify the behavior or appearance of
    - existing element
    - component
    - other directive
  - types:
    - `ngModel`
    - `ngClass`
    - `ngStyle`

## Structural Directives

### `*ngIf`

```html
<!-- only show form if both loginSuccess & loginFailed is false -->
 <!-- otherwise show element with the template variabel name messages -->
<form *ngIf="!loginSuccess && !loginFailed; else messages">
    <label for="userName">User Name</label>
    <input  type="text" name="userName" [(ngModel)]="userName">
    <label for="password">Password</label>
    <input type="password" name="password" [(ngModel)]="password">
  <button type="submit"  (click)="login()">Login</button>
</form>
<!-- template with template variable name #messages -->
<!-- template only gets rendered by angular if specifically instructed to render it -->
<!--in this case it only gets rendered if either loginsuccess or loginfailed is true --> 
<ng-template #messages>
    <!-- <ng-container> will only render if the login failed -->
    <ng-container *ngIf="loginFailed">
      <img src="loginfailed.png" alt="login failed">
      <h4 style="font-family: cursive;">Invalid Credentials</h4>
    <!-- this <ng-container> only renders in case of login success -->
    </ng-container>
    <ng-container *ngIf="loginSuccess">
      <img src="loginsuccess.png" alt="login successful">
      <h4 style="font-family: cursive;">Welcome {{userName}}!!</h4>
    </ng-container>
</ng-template>
```

- `<ng-template>` is a template that only gets rendered by angular if specifically instructed to render it.
- `<ng-container>` is a special element that can hold structural directives without adding a new element to the DOM

### `*ngFor`
> Used to iterate over a collection of data.

`app.component.ts`
```ts
export class AppComponent {
  courses: any[] = [
    { id: 1, name: "TypeScript" },
    { id: 2, name: "Angular" },
  ];
}
```
`app.component.html`
```html
<ul>
  <li *ngFor="let course of courses;  let i = index"> 
       {{i}} - {{ course.name }} 
  </li>
</ul>
```

## Attribute Directives
> Changes the appearance/behavior of a component/element. 

Types of built-in attributes directives
- ngStyle
- ngClass

### `ngStyle`
> Used to modify a component/element's style

- `[ngStyle] = "expression"`
- expression can accept 
  - array
  - string
  - object

```html
<p [ngClass]="{css_class_name1: boolean, css_class_name2: boolean}">
```
### `ngClass`
> Used to dynamically set or change the css classes for DOM element.

- `[ngClass] = "expression"`

template:
```html
<!-- setting classes with array of strings -->
<span [ngClass]="['blueColored', 'capitalized']">

<!-- setting css classes to true/false depending on -->
<!-- whether they are applicable or not -->
<!-- based on class variables -->
<span [ngClass]="{
    blueColored:isBlue,
    capitalized:isCapitalized
}">
```
where in component class:
```ts
class MyComponent {
  isBlue = true;
  isCapitalized = true;
  letItBlue = blueColored;
}
```
with css:
```css
.blueColored {color: blue;}
.capitalized { font-variant: small-caps;}
```

#### Property Binding with [ngClass]

```html
<!-- sets ngClass to class variable 'letItBlue' -->
<!-- class variable 'letItBlue' has the value 'blueColored' -->
<!-- blueColored is a CSS class name -->
<span [ngClass]="letItBlue">Used [ngClass] property styling</span>
```
See class and css above.

### [class] property binding (NOT [ngClass])

Sets specific classnames true or false using class variables.
```html
<span
    [class.blueColored]="isBlue"
    [class.capitalized]="isCapitalized"
>
```

## Custom Directives
> Custom Directives are used to change the appearance of the components.

Can be:
- Attribute Directive
- Structural Directive
 
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

### Custom Attribute Directives

Create a directive that changes a button's color when hovered over. Let's take the color to change to from an input box.

1. create directive with `ng g d cameleonButton`

`cameleon-button.directive.ts`
```ts
import { Directive, ElementRef, HostListener, Input, OnInit } from '@angular/core';

@Directive({
  selector: '[appCameleonButton]'
})
export class CameleonButtonDirective implements OnInit {

  // takes input for button color during hover over
  @Input()
  buttonColor?: string;
  // sets original background color
  originalColor = "black";

  // elementRef instance is injected to refer element
  // this attribute directive is applied to
  constructor(private elementRef:ElementRef) { }

  ngOnInit() {
    // set up styles for our element
    this.elementRef.nativeElement.style.backgroundColor = this.originalColor;
    this.elementRef.nativeElement.style.color = "white";
  }

  // listen to events on element
  // on mouseEnter set background color to color received
  @HostListener('mouseenter') 
  onMouseEnter() {
    this.elementRef.nativeElement.style.backgroundColor = this.buttonColor;
  }

  // on mouseLeave set background color to orginial color
  @HostListener('mouseleave')
  onMouseLeave() {
    this.elementRef.nativeElement.style.backgroundColor = this.originalColor;
  }
}
```

2. apply custome attribute directive to HTML element

`my-comp.component.html`
```html
<label>Enter button color for hover-over:</label>
<br>
<br>
<!-- [(ngModel)] binds value of input to color variable in component class-->
<input type="text" [(ngModel)]="color">
<br />
<br>
<!-- apply custom attribute directive to button element -->
<!-- use directive's selector to add it as an attribute  -->
<!-- [buttonColor] binds buttonColor in directive to color in component class -->
<button appCameleonButton [buttonColor]="color">Cameleon Button</button>
```

3. Store input value in component

`my-comp.component.ts`
```ts
import { Component } from '@angular/core';

@Component({
  selector: 'app-test-directive',
  templateUrl: './test-directive.component.html',
  styleUrls: ['./test-directive.component.css']
})
export class TestDirectiveComponent {

  // color variable used to set button background color when hovering over button
  color = "yellow";

}
```