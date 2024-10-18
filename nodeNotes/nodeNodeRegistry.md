# NPM Registry
> Collection of all the open source JS libraries in the world. [Software registry](https://www.npmjs.com/) maintained by Node.js


## Package Managers

Package managers working with the Node Registry
- NPM 
- YARN

## NPM
> Package manager for node.js

### package.json
- start projects with `npm init`
- creates a `package.json` file
- that holds metadata about the project

```json
{
  "name": "mypackage",
  "version": "1.0.0",
  "description": "\"Testing publishing\"",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
} 
```


### Install packages

`npm install <package-name>[@version]`

Installation types:
- global
    - uses `-g` flag
    - package gets added to the `PATH`
    - `npm install -g <package-name>`
- local


### Update Packages

- To update a global package:
    - `npm update -g <package-name>`

- To udpate a local package:
    - go to folder where package is installed
    - run `npm update`

### Uninstall Package

`npm uninstall -g <pacakge-name>[@version]`

## Publish to Node Registry

### 1 Create Account 
Create account on [npmjs.com](https://www.npmjs.com/)


### 2 Create module to publish

- create folder
- create package.json in the folder
- 
