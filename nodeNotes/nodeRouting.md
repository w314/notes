node, routing, routes

# Node.js Routing
> Routing is achieved using the `Request.url` property.


## Handling Routes
1. create routeHandler file 
    - that has a function to handle each route 
    - and create the appropriate response
    - or create several files to handle each route
2. create router file 
    - that would call the appropriate function of the routerHandler 
    - based on the url
3. in your server 
    - call your router 
    - and pass the request and response objects


### 1. Create RouterHandler JS file

`homePageHandler.js`
```js
// import fs module to read html file
import { readFile } from 'node:fs/promises';

// path of html file,  from root directory of project
const homeHtmlPath = './html/home.html';

// route handler function
const homePageHandler = async (req, res) => {
    try {
        // read html 
        const html = await readFile(homeHtmlPath, { encode: 'utf-8' });
        // send response with html read from homePage.html
        res.writeHead(200, { ContentType: 'text/html' });
        res.write(html);
        res.end();
    } catch (err) {
        // send error message in case of error
        console.log(err);
        res.writeHead(500);
        res.write('Error displaying page.')
        res.end();
    }
}

// export routeHandler
export default homePageHandler;
```

### 2. Create Router JS File
- Implements mapping logic.
- Based on the request url calls the appropriate function of the RouterHandler file

`Router.js`
```js
// import handlers
import loginHandler from './loginHandler.js';
import homePageHandler from './homePageHandler.js';
// import required modules
import * as url from 'url';

const router = (req, res) => {

    // parse url of the request object
    const reqUrl = url.parse(req.url);
    // get path from parsed url
    const path = reqUrl.path;
    console.log(path);

    // call appropriate handlers based on path
    switch(path) {
        case `/home`:
            homePageHandler(req, res);
            break;
        case `/login`:
            loginHandler(req, res);
            break;
        default:
            homePageHandler(req, res);
    }
}
// export router
export default router;
```

### 3. Call Router in Server
- call the router for each request
- pass the request and response objects

```js
import http from 'http';
// import your router
import router from './routes/router.js'

// create server
const server = http.createServer((req, res) => {

    // call router to handle request
    router(req, res);
});

// start server
const port = 3000;
server.listen(port);
console.log(`Server is listening on port ${port}`);
```