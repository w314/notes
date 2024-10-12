node, routing, routes

# Node.js Routing
> Routing is achieved using the `Request.url` property.


## Handling Routes

### 1. Create JS File to Implement Route Handler Logic

`RouteHandler.js`
```js
// load required modules
const DBModule = require('./DBModule');
const url = require('url');
const querystring = require('querystring');

// create function for each route 
// and attach it to the exports object

exports.greetUser = (url, request, response) => {
    // retrieve data from post request
    const data = "";
    request.on('data', ( chunk ) => data + chunk;);
    // generate response when all data received
    request.on('end', () => {
        // parse data
        query = querystring.parse(data);
        const name = query['name'];
        // send response
        response.writeHead(200, { ContentType: "text/html" });
        response.end(`<html><body><h1>Hello ${name}!</h1></body></html>`);
    })
}

exports.enterNmae = (url, req, res) => {
    // create response
    res.writeHead(200, { ContentType: "text/html" });
    const html = `
        <html>
            <body>
                <form name="myForm" action="http://localhost:7777/greetUser" method="post">
                    <label>Name</label>
                    <input type="text" name="name" value="">
                    <input type="submit" value="Sumit">
                </form>
            </body>
        </html>
    `;
    res.write(html);
    res.end();
}
```

### 2. Create JS File to Implement Route Mapping Logic

`GreeterRouting.js`
```js
// load required modules

