js, javascript, modules, node

# Node Modules

## Advantages:
- better code organization
    - can group realted code in separate js files
- better code maintainablity
- code reusability

## Built in Node Modules

- `http`
    - used to create web servers and handle web requests/response.
- `util`
    - provides utility functions
- `fs`
    - handles file related operations
- `net`
    - used to implement socket programming
- ... and more


## Loading Modules

- `export object` of the module loaded is returned
- export object can be used to access all method of the loaded module

### 1. using `require()` method
```js
// using name of core module file
const http = require('http');

// using system path to module
const moduleName = require('pathToModule');
```

### 2. using `import` 


## Creating Modules

### Ways To Create modules:
1. create js file same as module name
2. create folder same as module name with an `index.js` file in it
3. overriding exports object


### 1. Create Module with Module File

#### Create Module File `DBModule.js`:
```js
exports.authenticateUser = (username, password) => {
    if(username === "admin" && password === "admin") {
        return "Valid User";
    } else {
        return "Invalid User";
    }

```
- attach each reusable method to the `exports object`

#### Use Created Module File

`httpServer.js`
```js
// use module name to load built-in http module
const http = require('http');
// use module path to load our custom module
const authenticator = require('./DBModule.js');

const server = http.createServer((request, response) => {
    // use authenticateUser method of DBModule to authenticate user
    const userValidationResult = authenticator.authenticateUser("admin", "admin");

    response.writeHead(200, { ContenType: "text/html"});
    response.write(
        `<html>
            <body>
                <p>${userValidationResult}</p>
            </body>
        </html>
        `
    );
    response.end();
});

server.listen(3003);
```

### 2. Create Module with Module Folders

- create folder named `DBModule`
- create file name `index.js` inside folder
    - the name `index.js` is manadatory

When loading module in `webServer.js`:
```js
const module = require('./DBModule');

// when using use module name
const result = module.authenticateUser(username, password);
```

### 3. Create Module by Overriding Exports Object

Used when there is only a single function or object to be exported.

`DBModule.js`
```js
// instead of attaching function to exports
// override exports object 
module.exports = (username, password) => {
    // same function code
}
```

`webServer.js`
```js
const authenticator = require('./DBModule.js');

// when using use module name directly
const result = authenticator(username, password);
```
