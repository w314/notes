createdAt: "2021-04-22T15:41:51.162Z"
updatedAt: "2021-05-03T18:41:32.113Z"
type: "MARKDOWN_NOTE"
folder: "da8af2edc74fad1126ed"
title: "Node.js"
tags: []
content: '''
  # Node.js
  - [Node.js](https://nodejs.org/en/)
  - `Node.js` enables us to run javascript on the desktop. (vs only in the browser)
  - `Node.js` is a JavaScript runtime built on Chrome V8 JavaScript engine.
  - - install the latest LTS (long term support) version, even number versions are LTS's, odd ones are 'Current' versions which are only supported for 6 months
  - [GitHub - goldbergyoni/nodebestpractices: The Node.js best practices list (March 2021)](https://github.com/goldbergyoni/nodebestpractices#3-code-style-practices)
  
  
  
  ## npm
  - npm is a tool for managing project dependencies via the command line
  - also a website hosting third-party packages
    - [npm](https://www.npmjs.com/)
    - modules are shared as packages
    - core modules include: path, file system
    - modules are stored in the app's node_modules folder, which is created automatically when modules are installed
  - initializing npm will setup a `package.json` file
  - when installing any package a `package-lock.json` file is created, which contains information for the dependencies of the modules you create
  - no need to alter neither `node_modules` nor `package-lock.json`, both should be added to `.gitignore`
  
  
  
  ## to run JavaScript code
  - run `node` in the terminal to start a node.js REPL enivronment (Read Evaluate Print Loop) which will run javascript in your terminal. Use `ctrl + D` to exit
  - run `node path/to/file` to run a javascript file
    - when running files `.` references the index file, `node src/.` will run src/index.js
    - you can run files without adding the *.js* extention.  `node src/server.js` = `node src/server`
  
  ## error handling
  - [Errors \\| Node.js v16.0.0 Documentation](https://nodejs.org/api/errors.html)
  - [Better Error Handling In NodeJS With Error Classes — Smashing Magazine](https://www.smashingmagazine.com/2020/08/error-handling-nodejs-error-classes/)
  
  
  ## event loop
  - [The Node.js Event Loop, Timers, and process.nextTick() \\| Node.js](https://nodejs.org/en/docs/guides/event-loop-timers-and-nexttick/#:~:text=The%20event%20loop%20is%20what,operations%20executing%20in%20the%20background.)
  
  
  ## modules
  - write module and export it
  ```javascript
  const concat = (arr1, arr2) => {
      return [...arr1, ...arr2];
    };
    
  const cut3 = (arr) => {
      arr.splice(2, 1);
      return arr;
    };
    
  module.exports = {
    concat,
    cut3
  };
  ```
  
  - import module in the code they are used
  ```javascript
  const myModule = require('./myModule.js');
  // OR
  const { concat, cut3 } = require('./myModule.js')
  
  // use it by:
  const myArray = [1, 2, 3, 4]
  console.log(myModule.cut3(myArray));
  // OR
  console.log(cut3(myArray));
  ```
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
