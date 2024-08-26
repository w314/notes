html, xml
# HTML (Hyper Text Markup Language)
- hypertext : defines link between web pages
- markup language 
    -  is used to annotate text, so that the browser can interpret it and manipulate text accordingly 
    - the tags convey meaning and/or functionality to the content between the tags
- describes the structure of a web page
- HTML Syntax
    - elements
    - attributes (key-value pairs)


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

## Doctype Declaration
```html
<!DOCTYPE html>
```
 - not an HTML tag
 - doctype declaration
 - informs the browser what type of document we are displaying
 - the above one is for HTML5

 ## HTML Root Tag
 ```html
<!DOCTYPE html>
<html lang="en">

</html>
 ```
 - root tag, encloses the entire document
 - attribute `lang` sets the language the document is written in, can be used by search engines

### Head Tag
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

  <!-- set keywords for page -->
  <meta name="keywords" content="tutorial,HTML">

  <!-- refresh rate of 30 second -->
  <meta http-equiv="refresh" content="30">

  <meta charset="UTF-8">

  <meta name="viewport" content="width=device-width, initial-scale=1.0">


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
`Inline Element` 
  - will stretch to take up only as much space as its content
  - cannot contain block elements
  - typically represent styling accents

`Block Element` 
  - will stretch to take up the entire width of their container
  - typically represent structured portions of the document

## HTML Tags

### `<h1> to <h6>` 
- marks the beginning of a new section of the document
- commonly marked with an id, allowing an anchor (<a>) tag to jump to this part of the document
- block elements

### `<p>`

### `<a>` Anchor Tag

 Link to another webpage or to a different portion of the current webpage.
```html
<a href="https://www.google.com" target="_blank" download>Google</a>
```
Attributes (some of them at leas):
- `href`
  - sets the location to go to when clicked
  - can be a `#` followed by an id to jump to that section of the page
`target`: tells the browser where to open the linked document
  - `_blank`: in a new tab
  - `_parent`: in a parent frame
  - `_self`: in the same frame (Default)
  - `_top`: nn the full body of the window
  - `iFrameName`: In the iFrame with the same name
- `download`: specified that the file will be downloaded

### `<img>` Image Tag
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
- together they create a captioned figure
- used with an image in order to use the image as a figure and then provide some information about the image
- block elements

### `<details> and <summary>`
```html
<details>
  <summary>Epcot Center</summary>
  <p>Epcot is a theme park at...</p>
</details>
```
- together they create a titled collapsable section
- until the name of the section (determined by `<summary>`) is clicked on the detials are hidden
- `<summary>` is an inline element
- `<details>` is a block element


### `<br />`
- `<br>` also works
- line break
- block element

### `<hr />`
- `<hr>` also works
- horizontal line
- block element

### lists `<ol>, <ul> and <li>`
```html
<ul>
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ul>

<ol start="50">
  <li>Coffee</li>
  <li>Tea</li>
  <li>Milk</li>
</ol>
```
- all block elements
- can be nested
- `<li>` list item
- `<ul>` unordered list
- `<ol>` ordered list

### Page Section Tags
- all block elements
- `<header>` : Used to represent the header of a page
- `<footer>` : Used to represent the footer of a page
- `<section>` : Used to represent a break to the next portion of the document
- `<article>` : Used to represent a self-contained subdocument
- `<aside>` : Used to represent content related to the main page content but not necessary for full understanding

Non-Sematic section tags:
- `<div>`
  - subsection of a document, no semantic meaning
  - block element
- `<span>`
  - subcection of a document, no semantic meaning
  - inline element

### Table
```html
<table>
  <!-- Table HEAD -->
  <thead>
    <!-- Table CAPTION -->
    <caption>Monthly savings</caption>
    <tr>
      <!-- details use <th> tags -->
      <th>Month</th>
      <th>Savings</th>
    </tr>
  </thead>
  <!-- Table BODY -->
  <tbody>
    <tr>
      <!-- details use <td> tags -->
      <td>January</td>
      <td>$100</td>
    </tr>
    <tr>
      <td>February</td>
      <td>$80</td>
    </tr>
  </tbody>
  <!-- Table FOOTER -->
  <tfoot>
    <tr>
      <td>Sum</td>
      <td>$180</td>
    </tr>
  </tfoot>
</table>
```
- `<table>` is the only block element
- `colspan` attribute for `<th>` and `<td>` specifies how many columns this entry should take up


## `<form> and the <form>` tags
An HTML form collects information from input elements.

### Input Elements
```html

```


## `<input>` Input Element
The `<input>`element can be displayed in several ways, depending on the type attribute.

```html



```
## XML (Extensible Markup Language)
> Markup language designed to store and transprot data.

Differences from HTML:
- dynamic: allows users to define custom tags
- case sensitive
- does not allow errors
- closing tags are necessary

## HTML Questions
- What is the difference between XML , HTML & HTML5?
- Explain what you know about HTML?
- What does HTML stand for?
- What is HTML? What is it used for?  

- What does HTML tag syntax look like? 

- Element vs Attribute 

- Examples of Elements and Attributes?  

- What is the DOCTYPE declaration? 

- Know the general syntax for Tables and Ordered/Unordered Lists  

- Know the following HTML input types 

    - Text field 

    - Password 

    - Radio Buttons 

    - Checkboxes 

    - Submit button 

- Know these form-specific elements/attributes 

    - Label 

    - Name 

    - Value  

    - Placeholder 

 