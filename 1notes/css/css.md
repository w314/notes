css

# CSS

## How to attach style to HTML

## Box Model

## CSS Properties

## Responsive Web Design

## CSS Overview

## Selectors

- class
- id
- sibling
- element
- advanced

#### Pseudo Class Selector
> Pseudo Class Selector is used to specify the state of an element.

```css
div: hover {
    backgournd-color: blue;
}
```
#### Pseudo Element Selector
> Pseudo-elements allows to style the specified parts of an element that is not available under DOM tree.
- `selector::pseudo-element {property: value;}`
- `::first-letter`
- `::first-line`


## Animations



## Responsive Web Design

### Media Queries
Media queries allow you to customize the presentation of your web pages for a specific range of devices like mobile phones, tablets, desktops.
- it uses the `@media` rule to include a block of CSS properties only if a certain condition is true.
- it composed of a media type and expressions that check for the conditions of particular media features.

#### Syntax
- @media
- media types
- media features
- logical operators

```css
/* syntax */
@media not | only meaditype and (mediafeature and | or | not mediafeature) {}

/* example */
@media only screen and (max-width: 600px) {
  body {
    background-color: lightblue;
  }
}
```
`mediatype` can be:
- screen
- print
- all

`mediafeature` can target:
- viewport width: `width`
- device orientation: `orientation`
- screen resolution 
- ...

## Flexbox
>  Flexbox, is a one-dimensional layout method for arranging elements in rows or columns.

- has a flex container
- which has children, the flex items

### Flexbox Container Properties
```css
.container {
    /* enables flex content for its children */
    /* by default creates a box element */
    /* can be inline-flex for an inline element */
    display: flex;
    
    /* establishes main axis */
    /* the direction flex items flow */
    /* the deafult is ROW */
    flex-direction: row | row reverse | column | column-reverse;

    /* by default all children try to fit into the container */
    /* default is NOWRAP  */
    flex-wrap: nowrap | wrap | wrap-reverse;

    /* shorthand for flex-direction and flex-wrap */
    flex-flow: column wrap;

    /* defines alignment among the main axis */
    /* default is flex-start */
    justify-content: flex-start | flex-end | center .... ;

}
```


#### Flex Children Properties (flex items)
``` css
.flexItem {
    /* let's item appear NOT in the order it is in the source file */
    order: 5;
    
}
```

## Grid
