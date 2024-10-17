# File Operations in Node.js
> Handled by the `fs` module.

Types:
- promise based
- asynchronous (with callbacks)
- synchronous

[Source](https://nodejs.org/en/learn/manipulating-files/reading-files-with-nodejs)

## Promise Based 

### Read File with fs/promises

```js
// import readFile method
import { readFile } from 'node:fs/promises';

// path from root directory of project
const htmlPath = './html/login.html'

// variable to store login page's html
let html;

// getHtml function will read the content of the loginHtml file
// and store it in the html variable
const getHtml = async () => {
    try {
        // encode: encode: utf-8 will mark the file content as text
        html = await readFile(filePath, { encode: 'utf-8' });
    } catch (err) {
        console.log(err);
    }
}

// handler function will send response with html retrieved from loginHtml file
// function will be async, so we can use await when reading file content
const loginHandler = async (req, res) => {
    await getHtml();
    res.writeHead(200, { ContentType: 'text/html' });
    res.write(html);
    res.end();
}

// export loginHandler
export default loginHandler;
```
### Append File with fs/promises
Creates file if does not exists.

```js
import { appendFile } from 'node:fs/promises';

const logFile = './log.txt';
appendFile(logFile, `User ${username} logged in at ${new Date()}\n`);
```

## Asynchronous Methods

### `fs.readFile()`

- `fs.readFile(fileName[, options], callbackFunction);`
- data read will be stored in an internal buffer temporarily
- and will be passed to the callback function

```js
// load required modules
const fs = require('fs');

// callback function err and data
fs.readFile(file, function(err, fileContent) => {
    if(err) throw err;
    response.writeHead(200, { ContentType: "text/html" })
    response.write(html);
    response.end();
})
```

### `fs.writeFile()`

### `fs.appendFile()`


## Synchronous Methods

### `fs.readFileSync`
- does not take a callback function
- use case example: reading config file 