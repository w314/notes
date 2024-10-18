# File Operations in Node.js
> Handled by the `fs` module.

Types:
- promise based
- asynchronous (with callbacks)
- synchronous (does not take a callback)

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

### Write File with `fs/promises`
Creates file if does not exists.


```js
import { writeFile } from 'node:fs/promises';

const filePath = './writeTo.txt';
const content = 'bob here';

const writeToFile = async () => {
    try {
        await writeFile(filePath, content);
        console.log(`File is ready.`);
    } catch (err) {
        console.log(`Eror: ${err}`)
    }
}
writeToFile();

```
### Append File with fs/promises
Creates file if does not exists.

```js
import { appendFile } from 'node:fs/promises';

const filePath = './writeTo.txt';

const appendToFile = async (filePath, content) => {
    try {
        await appendFile(filePath, content);
        console.log(`File is content updated with: ${content}`);
    } catch (err) {
        console.log(`Eror: ${err}`)
    }
}

for(let i = 0; i < 3; i++) {
    const content = `Updated at ${new Date()}\n`;
    appendToFile(filePath, content);
}
```