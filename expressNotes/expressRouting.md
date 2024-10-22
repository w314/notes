# Express Routing

>Routing is defining endpoints of the application and the way the application responds to requests to those endpoints.

## Routing in Express

- via applications object
- using express.Router class

## `express.Router` class

### 1. Create routeHandlers
controller/`userHandler.js`
```js
export getUser = (req, res) => {
    try {
        res.status(200)json({
            message: 'User is found'
        });
    } catch (err) {
        res.status(404).json({
            status: 'fail',
            message: err
        })
    }
};

export addUser = (req, res) => {

}
```

### 2. create router

`router.js`
```js
import express from 'express'
// import route handlers
import * as userHandler from './userHandler.js'

const router = express.Router();
router.get('/user', userHanddler.getUser);
rotuer.post('/user', userHandler.postUser);
// make all other endpoints invalid
router.all('*', userHandler.invalid);

export router
```

### 3. user router in app.js
`app.js`
```js
import express from 'express'
// import router
import router from './router'

const app = express();
// set up router
app.use('/', router);

// ... 
```



### Route parameters

#### `req.params`

From URL `/user/:username/:id`
```js
const getUser = (req, res) => {
    const username = req.params.usernam;e
    const id = req.params.id
    res.send(`Welcome ${username} with id ${id}`);
}
```

#### `req.query`

From url `/user?name=bob&age=2`

```js
const getChild = (req, res) => {
    const name = req.query.name;
    const age = req.query.age;
    res.send(`Hi ${name}, you are ${age}!`)
}