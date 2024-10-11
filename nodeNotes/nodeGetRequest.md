node, get, request

# Handling GET Requests with Node

- with `GET` requests, data will be attached to the `url`
- built-in modules to handle GET requests:
    -  `url` module
    -  `querystring` module
- the `Request Object` will be holding the data sent by the client


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
    
    // get querystring from url
    const query = url.parse(req.url).query;
    console.log(`querystring: ${query}`);

    // get parameters from query
    const username = querystring.parse(query)["username"];
    const password = querystring.parse(query)["password"];

    //send response
    res.writeHead(200, { ContentType: "text/html" })
    res.write(`<html><body><h1>Hi ${username}!</h1></body></html>`);
    res.end();
}

// use function when creating server
http.createServer(onRequest).listen(7777);
```
