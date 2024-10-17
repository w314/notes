html, form

# Form Element

```html
<form name="Name of the form" action="Link to server-side program" method="HTTP Request method" target="Where to display the response">
    <!-- All the form elements will come here-->
</form>
```

## Form Action

### Passing data through url

```html
<!-- form will create a GET request -->
<!-- form will pass data in the urls as query string -->
<!-- localhost:3000?username=nameEntered?password=pwdEntered -->
<form action="http://localhost:3000">
    <label for="username">Username:</label>
    <!-- without the name attribute no data data is passed -->
    <!-- data is indentified based on the name attribute -->
    <input type="text" id="username" name="username">
    <label for="password">Password</label>
    <input type="password" id="password" name="password">
    <input type="submit" value="Login">
</form>
```
- this form will create a `GET` request
- this form will pass data to server in the url
- `http://localhost:3000?username=nameEntered&password=passwordEntered`
- the `name` attribute of the `input element` is necessary for the data to be passed in the url and are identify the data

### passing data through request body

```html
<form action="http://localhost:3000" method="post">
    <!-- form fields -->
</form>
```
- add `method="post"` attribute to `form` tag
- `name` attributes of `input` elements still identify the data in the form

### From Element Attributes
- **name**
    - unique name for form
    - used for accessing the form data
- **action** 
    -  URL of destination page
- **method** attribute 
    - HTTP request method
    - default is GET, data will be appended to the URL
    - in case of POST, data is sent in request body.
- **novalidate**
    - skips validation upon submission
- **target** 
    - specifies where to display the response

## Input Element

### Input Element Types

- `text`	Creates a string input field.
- `password`	Creates a password input field in masked format
- `radio`	Creates a radio button.
- `checkbox`	Creates a checkbox
- `button`	Creates a simple button
- `submit`	Creates a button to submit the form.
- `reset`	Creates a button to reset form fields.
New in HTML5
- `date`	Input represents date(year, month, date) value without time zone
- `email`	Input represents an email address value
- `number`	Input represents a numerical value.
- `url`	Input represents URL address value.
- `file`	Input that lets the user select a file.
- `color`	Input that lets the user choose a color.
- `range`	Input that lets the user choose a number from a range.

### Input Element Attributes

required	Value required for form submission.
value	Specifies default value of input element.
type	Identifies type of input element.
name 	Name of input element used for form submission.
size	Identifies the width of input text that the user can see.
autofocus	Focuses on a particular form element automatically.
maxlength	Identifies the maximum length of input value.
minlength	Identifies the minimum length of input value.
pattern	Specifies a pattern (regular expression) for entering input text. 
placeholder	Displays a text (hint) within an input control for the user.
steps	Specifies the legal number of intervals.
- `formnovalidate`	skips validations upon form submission, used with submit button. 
readonly	Prevents user from modifying the value, value will passed on submit
disabled	Prevents from modifying the value, value is not sent on submit
multiple	 allows to enter/select more than one value

## Select
```html
<label for="dropdown_list">Dropdown</label>
<select id="dropdown_list">
   <option>option 1</option>
   <option>option 2</option>
</select>
```


### Select Attributes
autofocus	Focuses on a particular input element of a form automatically.
name	Name of the select element.
disabled	Disables the dropdown.
multiple	Select multiple options from the dropdown list.
size	Value of size decides the number of visible options in dropdown.


## Datalist Element

> `<datalist>` is used to provide predefined values for the input field.

```html
<label for="stream">Choose your stream</label>
<input list="streams" name="stream" id="stream" />
<datalist id="streams">
    <option value="Java">
    <option value="UI">
    <option value="BigData">
    <option value="IMS">
    <option value="AI">
</datalist>
```
- `<input>` has to have `list` attribute where the value is the `id` of the `<datalist>`
- `<datalist>` vs. `<select>`: the `<datalist>` is used for autocomplete and we can edit the value
- as you start to enter values in the input box, it searches the datalist values based on the input

## `<textarea>`
```html

<label for="textarea">Textarea</label>
<textarea id="textarea" rows="2" cols="15">
</textarea>
```


## `<a>` Anchor Element

User the `rel` attribute for security:
```html
<p>To visit Lex<a href="http://lex.infosysapps.com" target="_blank" rel="noreferrer noopener">Go to Lex</a></p>
```
When a link opens the URL in a new tab with target="_blank", it is very simple for the opened page to change the location of the original page because of usage of the JavaScript variable window. The Opener will not be null and thus "window.opener.location" can be set by the opened page. This exposes the user's information to phishing attacks. Hence security aspects with respect to this have to be taken care while developing applications. The simplest way to achieve security is to use rel attribute of anchor element. 

## `<audio>` Audio Element

```html
<audio src="link of the audio file" controls="controls">Your browser does not support the audio tag</audio>
```
- Content between <audio> and </audio> tag will be shown by browsers who do not support audio element.
- if `<audio>` tag is given a video src, it will play the audio part without any erros
### `<audio>` attributes
src	Specifies the URL of the media resource
controls	Media control feature like play/pause will be displayed
loop	Causes the media to play in a loop
autoplay	Media will play automatically on page load
muted 	Media will play in muted state


## `<video>` Video ELement
```html
<video src="myVideo.mp4" controls="controls" poster="firstFrame.png">Your browser does not support the video tag</video>
```
Content between <video> and </video> tag will be shown by browsers who do not support video element.


### `<video>` Attributes
src	Specifies the URL of the media resource
controls	Media control feature like play/pause will be displayed
loop	Causes the media to play in a loop
autoplay	Media will play automatically on page load
muted 	Media will play in muted state
width 	Specifies the width of the image in pixels
height	Specifies the height of the image in pixels
Poster	Representative frame for the video till the video is played

## `<source>` Element
All browsers don’t support all image/audio/video formats. Therefore you must list multiple sources of audio/video element of various formats. 
- the `<source>` element is considered only when `src` attribute of media element is absent
- You must list different media sources in order - most desirable to least desirable.

```html
<audio>
    <source src="myAudio.mp3" type="audio/mp3" >
    <source src="myAudio.ogg" type="audio/ogg" >
</audio>


<video>
    <source src="myAudio.mp4" type="video/mp4">
    <source src="myAudio.ogg" type="video/ogg" codecs="theora,vorbis" >
</video>
```

 The `codecs` attribute is used to specify version of the codecs needed to play the audio or video file.

