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
// http://localhost:7777/login?usrname="bob"&&password="123"
function onRequest(req, res) {
    
    // use the parse method of the url module 
    // to get querystring from the url
    // request.url property has the value of the url
    const reqQuery = url.parse(req.url).query;
    console.log(`querystring: ${query}`);

    // use parse() method of querystring
    // to get parameters from querystring
    const username = querystring.parse(reqQuery)["username"];
    const password = querystring.parse(reqQuery)["password"];

    //send response
    res.writeHead(200, { ContentType: "text/html" })
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
const DBModule = require('./DBModule');
const querystring = require('querystring');

// create server
const server = http.createServer( (req, res) => {

    // temporary data variable to store incoming data chuncks
    const data = "";

    // set function to handle data event
    req.on('data', ( chunk ) => data + chunnk );
    
    // set function to handle end event 
    // end even will get fired after all data chunks are received
    req.on('end', () => {
        // parse query from  data with querystring module
        const query = querystring.parse(data);
        // get data from query
        const username = query['username'];
        const password = query['password'];

        // authenticate user using DBModule
        const userStatus = DBModule.authenticateUser(username, password);

        // send response
        res.writeHead(200, { ContentType: "text/html" });
        // it is possible to give end the content 
        // and to not use res.write()
        res.end(`<html><body><h1>${userStatus}</h1></body></html>`);
    })
});

// start server
server.listen(3008);
console.log(`Server listening on port 3008`);
```

## URL module

```js
var path = url.parse(request.url).pathName