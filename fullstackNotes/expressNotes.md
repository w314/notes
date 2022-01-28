express nodemon nodejs middleware

  # Express
  [Express - Node.js web application framework](https://expressjs.com/)
  
  ## Installation & Setup with Node.js
  ```bash
  npm i express
  npm i --save-dev @types/express nodemon
  ```
  - **@types/express** types for TypeScript
  - **nodemon** will restart the server after every save
  
  #### Add script to `package.json`
  ```javascript
  "scripts": {
    "start": "nodemon src/index.ts"
  }
  ```
  
  ## To create a server with express
  - import express
  - create application object
  - listen on a port
  
  In the `src/index.ts` file:
  ```typescript
  import express from 'express'
  
  const app = express();
  const port = 3000;  //can be any number > 1024
  
  // define routes
  app.get('/api', (req, res) => {
    res.send('server working');
  });
  
  // start the server
  app.listen(port, () => {
    console.log(`Server started at http://localhost:${port}`);
  });
  
  ```
  ## Routes
  We handle our endpoints with routes and separate them from our server.
  - create a directory for `routes` under `/src`
  - create main route index file in this routes directory
  - create individual files for each route under `routes/api`
  - update application entrypoint index.ts to use routes
  
  
  Individual route file `src/routes/api/frogs.ts`:
  ```typescript
  import express from 'express'
  
  //create router object
  const frogs = express.Router();
  //set up route
  frogs.get('/', (req, res) => {
      res.send('frogs page');
  });
  //export route
  export default frogs;
  ```
  ```typescript
  import express from 'express'
  
  //create router object
  const sampleRoute = express.Router();
  //set up route
  sampleRoute.get('/', (req, res) => {
      res.send('Application starting page');
  });
  //export route
  export default sampleRoute;
  ```
  
  
  
  Main router index file `src/routes/index.ts`
  ```typescript
  import express from 'express'
  //import your routes
  import sampleRoute from './api/sampleRoute'
  
  //create router object
  const routes = express.Router();
  
  //set up router object to use your routes
  routes.use('/sampleRoute', sampleRoute); 
  
  //export router object
  export default routes;
  ```
  
  Update main application entrypont file `/src/index.ts`
  ```typescript
  import express from 'express'
  //import routes
  import routes from './routes/index'
  
  //create the server and set the port
  const app = express();
  const port = 3000;
  
  //setup your app to use the router
  app.use('./api', routes);
  
  //start the server
  app.listen(port, () => {
    console.log(`Server started at http://localhost:${port}/api/sampleRoute`);
  });
  ```
  
  ## Middleware
  [Express middleware: A complete guide - LogRocket Blog](https://blog.logrocket.com/express-middleware-a-complete-guide/)
  Middleware is a function applied between the reqest and the response. You can use one or several middleware functions.
  
  - used on application / route level
  ```typescript
  const middleware = [cors, logger];
  app.use(middleware);
  ```
  - used on endpoint level
  ```typescript
  const middleware = [cors, logger];
  frogs.get('/', middleware, (req, ,res) => {
    // do sutff
  });
  ```
  
  - middleware function 
  ```typescript
  // takes 3 required parameters
  // optional err parameter can be an error handler
  const myMiddleware = (req: express.Request, res: express.Response, next: Function): void => {
      console.log(req.query.product);
      // next() is an express router method, it calls the next middleware
      next();
  };
  ```
  
  ## About Request Object 
  ### Getting url of request:
  *req.url is not a native Express property, it is inherited from Node’s http module. Be aware the “mounting” feature of app.use() will rewrite req.url to strip the mount point.*
  
  To get the URL use:
  ```javascript
  app.use('/admin', function (req, res, next) { // GET 'http://www.example.com/admin/new?sort=desc'
    console.dir(req.originalUrl) // '/admin/new?sort=desc'
    console.dir(req.baseUrl) // '/admin'
    console.dir(req.path) // '/new'
    next()
  })
  ```
  
  ## Working with files
  
  ```javascript
  import {promises as fs} from 'fs'
  
  const filePath = ''
  
  
  ```
'''
linesHighlighted: [
  35
  49
]
isStarred: false
isTrashed: false
