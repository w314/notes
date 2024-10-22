# Session Management in Express

## Usign Cookies with cookieParser
> cookieParser middleware provided by express parses cokies and attaches them to the request object.

Install with:

`npm install cookie-parser`

Use in `app.js`

```js
import cookie-parser from 'cookie-parser';

const app = express();

app.use(cookie-parser());
```

## express session
> Stores data on the server side


