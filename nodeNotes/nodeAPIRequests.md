node, get, request

# Handling API Requests with Node

## GET Requests

- with `GET` requests, data will be attached to the `url`
- built-in modules to handle GET requests:
    -  `url` module
    -  `querystring` module
- the `Request Object` will be holding the data sent by the client
- the `request.url porperty` contains the url of the request

## Example
Processing GET request from user:<br>
 `http://localhost:7777/login?usrname="bob"&&password="123"`

```js
// load modules needed for user data process
const http = require('http');
const url = require('url');
const querystring = require('querystring');

// server method that will handle get request like:
function onRequest(req, res) {
    
    // RETRIEVE DATA SENT IN URL
    // get url from url property of request
    const reqUrl = req.url;
    console.log(`Request URL: ${reqUrl}`);
    // use url module to parse url and 
    // get querystring from the query property
    const reqQuery = url.parse(reqUrl).query;
    console.log(`Request querystring: ${reqQuery}`);
    // use querystring module to parse querystring
    // get data from parsed querystring
    const username = querystring.parse(reqQuery)['username'];
    const password = querystring.parse(reqQuery)['password'];
    console.log(`Username: ${username}\nPassword: ${password}`);

    //send response
    res.writeHead(200, { "Content-Type": "text/html" })
    res.write(`<html><body><h1>Hi ${username}!</h1></body></html>`);
    res.end();
}

// use function when creating server
http.createServer(onRequest).listen(7777);
```


## Post Requests

- handling post requests is done using Event Handling
- see Event Handling in `nodeNotes/nodeEvents.md`
- use `data` and `end` events of the `request object`
- utilizes the `querystring` built in module
- data is sent in request body


Handling POST requet coming to url: `http://localhost:7777`<br>
With requestBody username and password.
```js
// load required modules
const http = require('http');
const dbModule = require('./DBModule');
const querystring = require('querystring');

// create server
const server = http.createServer( (req, res) => {

    // RETRIEVE DATA FROM REQUEST

    // create variable to store incoming data chunks
    const data = "";

    // set function to handle data event
    // add each incoming data chunk to our data variable
    req.on('data', ( chunk ) => data + chunnk );
    
    // set function to handle end event 
    // end even will get fired after all data chunks are received
    req.on('end', () => {
        // parse received request data with querystring module
        const reqData = querystring.parse(data);
        // get username and password from parsed request data
        const username = reqData['username'];
        const password = reqData['password'];

        // authenticate user using DBModule
        const userStatus = dbModule.authenticateUser(username, password);

        // send response
        res.writeHead(200, { "Content-Type": "text/html" });
        // it is possible to give end the content 
        // and to not use res.write()
        res.end(`<html><body><h1>${userStatus}</h1></body></html>`);
    })
});

// start server
server.listen(3008);
console.log(`Server listening on port 3008`);
```

## Sending Non-Text Response

### JSON Response

```js
import { readFile } from 'node:fs/promies'

const jsonHandler = async (req, res) => {
    const filePath = './content.json'
    const jsonContent = await readFile(filePath, { "encode": "utf-8" });
    res.writeHead(200, { "Content-Type": "application/json" });
    res.write(jsonContent);
    res.end();
}
```

### IMG response
```js
import url from 'url';
import { readFile } from 'node:fs/promises'

const imageHandler = async (req, res) => {

    // get request path
    const reqUrl = url.parse(req.url);
    const path = reqUrl.path;

    // read image from file
    const filePath = `./books/images${path}`
    const img = await readFile(filePath);

    // write response
    res.writeHead(200, { "Content-Type": "image/jpg" });
    res.write(img);
    res.end();
}

export default imageHandler;
```