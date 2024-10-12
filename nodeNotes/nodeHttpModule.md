node, nodejs, web-server, http

# Node Web Server with `http` Module

`http` module is provided by Node, we can use it to create a web server.

`webServer.js`
```js
// import http module
// can only used from a module
// import http from http;

// require module
const http = require('http');

// create a web server
// takes a function as a parameter
// this callback function executes for every request received
// callback function accepts a request and a response object as arugemnts.
const server = http.createServer((request, response) => {

    // send header information
    // status code and header information
    response.writeHead(200, { 
        ContentType: "text/html"
    });

    // send response data
    response.write(
        `<html>
            <body>
                <h1>Hello From Node Server</h1>
            </body>
        </html>
        `
    );

    // end response after data is sent
    response.end();
})

// start server
// provide port number as argument
const port = 3000;
server.listen(port);
```
- run server with `node webServer.js`
- access it in the browser with url `localhost:3000`
- response content can also be sent by `response.end()`
    - it sets content
    - ends the response
    - NO need for `response.write()`
    
## Other Methods

`response.send()` 
- writes the response content and ends the response.
- no need for respones.end()