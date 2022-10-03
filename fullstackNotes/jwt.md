json web token, jwt

# JWT
> never store sensitive information in a jwt
- jwt created by a `base_64` algorithm, that just jumbles up text in a standard way, anybody can produce a `jwt` like token easily
- jwt has 3 parts
    - header
    - payload
    - signature
- jwt has to answer:
    1. who made the request:  that information is in the `payload`
    1. can we trust the information provided: `signature` should show us


## How `signature` is used
- The `signature` is created by using our `header`, `payload` and a `TOKEN_SECRET` secret variable stored on in our authentication service and the server that needs to validate the `jwt` 
- As the `signature` contains the `payload` and `header`, if those two would be changed en route will recognise that the data was tampered with.


## Use `jwt` in a `nodejs` app

### 1. Install `JWT`
```bash
# install jwt
npm i jsonwebtoken
# install typescript types for jwt
npm i --save-dev @types/jsonwebtoken
```

### 2. Add new environmental variable to `.env` file
```bash
TOKEN_SECRET=verySecretToken
```

### 3. Create Token
`jwt.sign(<objectToIncludeInToken>, <TOKEN_SECRET>)`
```typescript
// import jwt
import jsonwebtoken from 'jsonwebtoken'
// import dotenv to handle environmental variables
import dotenv from 'dotenv'

// get TOKEN_SECRET environmental variable
dotenv.config()
const TOKEN_SECRET: string = process.env.TOKEN_SECRET as string

// create token
// pass object to store in payload as first parameter
const token = jsonwebtoken.sign({user: myUser}, TOKEN_SECRET)
```

### Check a token
`jwt.verify()`
