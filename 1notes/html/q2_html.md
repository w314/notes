html

# HTML (Hyper Text Markup Language)

- describes the structure of a web page
- not a programming language
- markup language 
    - uses tags to convey more meaning and/or functionality to the content between the tags
    - browser will interpret the markup
- HTML Syntax
    - elements
    - attributes

## HTML Document Structure
```html
<!-- doctype declaration -->
<!--  -->
<!DOCTYPE html>
<html>
    <head>
    </head>
    <body>
    </body>
</html>
```

### Doctype Declaration
```html
<!DOCTYPE html>
```
 - not an HTML tag
 - doctype declaration
 - informs the browser what type of document we are displaying
 - the above one is for HTML5

 #### HTML Root Tag
 ```html
<!DOCTYPE html>
<html lang="en">

</html>
 ```
 - root tag, encloses the entire document
 - attribute `lang` sets the language the document is written in, can be used by search engines

#### Head Tag
```html
<!DOCTYPE html>
<html lang="en">
  <head>

    <!-- to name the browswer tab -->
    <title>Hello World</title> 
    
    <!-- to define internal CSS stylesheet -->
    <style></style>
   
   <!-- to describe various pieces of information about 
   the webpage to the search engine -->
    <meta /> 

    <!-- to link external resource like CSS stylesheet -->
   <link />

    <!-- o specify alternate content to be displayed 
    to users who have scripts disabled or 
    are on a browser that doesn't support scripts, 
    can also be used in the <body>. -->
   <noscript></noscript>

    <!-- to link an external JavaScript file -->
    <script></script>

    <!-- to specify a default URL and target setting for all links -->
    <base />

  </head>
</html>
```
- contains metadata (information aobut the webpage)
- place to put non-rendering tags (ones that does not get displayed on the webpage)
- HOWEVER regular tags (eg: `<h1>`) placed into the `<head>` section WOULD render

### Body Tag
```html
<!DOCTYPE html>
<html lang="en">
  <head></head>
  <body>
    <h1>Page Content</h1>
  </body>
</html>
```
- holds page content

## DOM (Document Object Model)
>The Document Object Model (DOM) represents the structure of a document in memory.
- represents the document as a node tree
- each node contains objects
- DOM methods allow programmatic access to the tree. With them, you can change the document's structure, style, or content.
- nodes can also have event handlers attached to them. Once an event is triggered, the event handlers get executed.

## HTML ELements
- tags have both structure and purpose 
- ensuring we use tags for their specific purpose is    `semantic markup`
- semantic markup is important because it conveys meaning of the webpage to assistive technologies


Part of element:
- opening tag
- content (unless contentless)
- closing tag (unless self closing)

### Inline vs Block Elements

## HTML Tags

### `<h1> to <h6>` 
- marks the beginning of a new section of the document
- commonly marked with an id, allowing an anchor (<a>) tag to jump to this part of the document
- block elements

### `<p>`


### `<img>
```html
<img 
    src="picture.jpg" 
    alt="Cat picture." 
    width="200px" 
    height="200px
>
```
- display picture on the webpage
- inline element
- self closing
- contentless

### `<figure> and <figcaption>`
``` html
<figure>
  <img src="pic_trulli.jpg" alt="Trulli">
  <figcaption>Fig.1 - Trulli, Puglia, Italy.</figcaption>
</figure>
```

<details> and <summary>
<br />
<hr />
<table>, <tr>, <th>, <td> and <caption>
<ol>, <ul> and <li>
<div>
<span>
<a>
<form> and the <form> tags


## Input elements and types




# HTML Questions

HTML 

What is HTML? What is it used for?  

What does HTML tag syntax look like? 

Element vs Attribute 

Examples of Elements and Attributes?  

What is the DOCTYPE declaration? 

Know the general syntax for Tables and Ordered/Unordered Lists  

Know the following HTML input types 

Text field 

Password 

Radio Buttons 

Checkboxes 

Submit button 

Know these form-specific elements/attributes 

Label 

Name 

Value  

Placeholder 

 