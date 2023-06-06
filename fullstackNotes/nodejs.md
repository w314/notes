nodejs npm

# [Node.js](https://nodejs.org/en/)

## READ

- [Node.js project architecture](https://softwareontheroad.com/ideal-nodejs-project-structure/)
- [The 12 factor app](https://12factor.net/)

## Install

### Linux - Install latest version

`Ubuntu` package manager doesn't have the latest version. To install:

- install [NVM](https://github.com/nvm-sh/nvm) _(Node Version Manager)_

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
```

Running the script first without the `| bash` will show what the script will do

- Restart Terminal
- Check installation

```
nvm --version
```

- install latest supported version

```bash
nvm install --lts
```

## [Working with files in Node.js](https://nodejs.dev/en/learn/working-with-folders-in-nodejs/)

```js
// import the fs module
const fs = require("fs");

// returns array of directory content
// with realtive path of content
fs.readdirSync(".");

// checks for file or directory
fs.lstatSync("./test.js").isFile();

// get full path of file or directory
const fullPath = fs.path.join(<folderPath>, <fileName>)
```
