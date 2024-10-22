# Express Middleware
> Handles cross-cutting concerns applicable to the entire applciations.

- authentications
- logging
- request body parsing

Benefits include better code organization.

Argumenst of a middleware function
- request
- response
- next
    - let's express know that middleware function finished executing

## Usage

Example middleware `myLogger.js` 
```js
const myLogger = (req, res, next) => {
    // performs logging function
    console.log(new Date(), req.method, req.url);
    // tells express that the middleware
    // is done with execution
    next();
}
```

To use  middleware in `app.js`

`app.use(<path>, <callback>)`
- path
    - optional 
    - sets the routes the middleware shoudl be used
    - if omitted it will be used for all routes
- callback
    - required parameter
    - middlware function to call

Or callback function can be provided directly:
```js
app.use('/login', (req, res, next) => {
  console.log(new Date(), req.method, req.url);
  next();
});
```

## Ordering

Order of execution of middleware depends on the order of the functions declared in the application.
```js
app.get('/', myController.getMethod);
app.use(myLogger);
app.post('/', myController.postMethod)
```
^ Logger middleware will ONLY be used for POST requests.