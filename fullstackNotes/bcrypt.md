# [bcrypt](https://www.npmjs.com/package/bcrypt) 
For password hashing

- `bcrypt` adds a secret string `pepper` to the passwords before hashing it
- adding the extra string makes it impossible to use passwords stolen from other systems in ours even if the passwords are the same
- it can aslo be set how many times passwords should be hashed `salt rounds` 
- has sync and async version of its functions

## How To Use in `node.js` app
- [Usage in Nodejs](https://www.abeautifulsite.net/posts/hashing-passwords-with-nodejs-and-bcrypt)

### Install 
```bash
npm i bcrypt
npm i --save-dev @types/bcrypt
```
## Set enviromental variables
- make sure the the following enviromental variables are included in `.env` file
- use `dotenv` to allow the project to use environmental variables
```bash

## for bcrypt ##
#extra string added to passwords before hashing
BCRYPT_PASSWORD=secretBcryptPass
# number of times password will be hashed
SALT_ROUNDS=10
```
- `SALT_ROUNDS` is the number of time the password will be hashed.
- `BCRYPT_PASSWORD` is the extra string added to the passwords before hashing

## Encrypt password

```javascript
const hash = bcrypt.hashSync(
    userPassword + BCRYPT_PASSWORD, 
    parseInt(SALT_ROUNDS)
)
```
- `hashSync` funcstion is syncronous
- takes two arguments 
    - string to hash: password + our secret string
    - number of times to hash: `salt rounds`
- we store the created `hash` in our database as password


## Validate password

```javascript
bcrypt.compareSync(
    passwordEntered + BCRYPT_PASSWORD,
    passwordInDatabase
)
```
- the function is synchronous

