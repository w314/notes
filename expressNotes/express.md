# Express.js

> Framework for creating web abbplication in Node.js

## Install express

`npm install express`



## Create basic server

```js
// import express
import express from 'express';

// create express application object
const app = express();

// setup server to listen for get requests
app.get('/', (req, res) => {
    res.send('Server is listening');
})

// get port from environmental variables
// keep environmental variables in .env file
const port = process.env.port;
// start server
app.listen(port, () => {
    console.log(`Server is listening on port ${port}`)
});


```



