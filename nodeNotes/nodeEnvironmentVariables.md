# Environment Variables in Node.js

## using `dotenv`

> Node module that loads environment variables from `.env` file into `process.env`

Install with:

`npm install dotenv --save`

Use:

```js
// import dotenv
import dotenv from 'dotenv';

// load environment variables
dotenv.config();

// use environment variables
const port = process.env.PORT
```

Without dotenv `process.env.PORT` will be undefined and the `.env` file has to be set as the environment variables file separately.


