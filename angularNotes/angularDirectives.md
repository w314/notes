angular, directive
# Angular Directives

What is a directive?

> Instructions for the DOM on how to build the web page.

 

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