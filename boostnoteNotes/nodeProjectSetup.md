createdAt: "2020-01-18T00:16:49.145Z"
updatedAt: "2021-07-20T23:48:10.220Z"
type: "MARKDOWN_NOTE"
folder: "7b7225fb954665754643"
title: "Node Project Setup with prettier, eslint, typescript"
tags: [
  "node"
  "eslint"
  "prettier"
  "TypeScript"
]
content: '''
  # Node Project Setup with prettier, eslint, typescript
  
  
  ## About ESlint and Prettier
  [How to use Prettier with ESLint and TypeScript in VSCode \\| Khalil Stemmler](https://khalilstemmler.com/blogs/tooling/prettier/)
  Prettier can automatically correct your files at every save or whenever when you run it directly.
  When using it together wiht ESLint, ESLint defines the code conventions and Prettier preforms the auto correcting based on the ESLint rules.
  
  
  ## Start Project
  
  #### Create a project directory
  - create an `src` directory for you `.ts` files
  - add an `index.ts` file under your `./src` as your starter file
  - and a `build` directory to store you compiled `.js` files
  ```shell
  mkdir src
  mkdir build
  touch ./src/index.ts
  
  ```
  
  #### Initate your node project
  - go to you project in the terminal
  - run `npm init` (or `npm init -y` to accept all defaults)
  - npm init will create your `package.json` file
    - A documentation for what packages your project depends on, allows you to specify the versions of the packages
    - It makes your build reproducable, easier to share with other
  - as you go through creating your package.json file:
    -  define the `entry point:` as your starter file here: index.html 
    -  add you github repository if wanted
    -  when ready accept the file with pressing enter
  
  
  
  ## Add  `eslint`, `typescript` and `prettier`
  [Using ESLint and Prettier in a TypeScript Project](https://robertcooper.me/post/using-eslint-and-prettier-in-a-typescript-project)
  
  ### install modules
  `typescript`
  ```bash
  npm i --save-dev typescript ts-node @types/node
  ```
  - **ts-node** TypeScript execution and REPL for node.js
  - **@types/node** contains type definition for node.js
  
  `eslint` 
  ```bash
  npm i --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
  ```
  - **eslint**: The core ESLint linting library
  - **@typescript-eslint/parser**: The parser that will allow ESLint to lint TypeScript code
  - **@typescript-eslint/eslint-plugin**: A plugin that contains a bunch of ESLint rules that are TypeScript specific
  
  `prettier`
  [Prettier · Opinionated Code Formatter](https://prettier.io/)
  ```bash
  npm i --save-dev prettier eslint-config-prettier eslint-plugin-prettier
  ```
  - **prettier**: The core prettier library
  - **eslint-config-prettier**: Turns off all ESLint rules that have the potential to interfere with Prettier rules.
  - **eslint-plugin-prettier**: Turns Prettier rules into ESLint rules.
  
  
  ### add configuration files
  `typescript`
  The configuraton file can be named **tsconfig.json** or **jsconfig.json**. To install the config file, run:
  ```bash
  npx tsc --init
  ```
  Useful settings:
  ```javascript
  {
    "compilerOptions": {
      "target": "es5",                          
      "module": "commonjs",                     
      "lib": ["ES2018", "DOM"], 
      "outDir": "./build",                        
      "strict": true,                           
      "noImplicitAny": true,                 
    },
    "exclude": ["node_modules", "tests"]
  }
  ```
  
  `.eslintrc.js`
  
  Add an *.eslintrc.js* configuration file in the **project root directory**. The JavaScript format adds the possibility to add comment vs the JSON format.
  ```javascript
  echo '{
    "root": true,
    "parser": "@typescript-eslint/parser",
    "plugins": [
      "@typescript-eslint",
      "prettier"
    ],
    "extends": [
      "eslint:recommended",
      "plugin:@typescript-eslint/eslint-recommended",
      "plugin:@typescript-eslint/recommended",
      "prettier"
    ],
    "rules": {
      "no-console": 'off',
      "prettier/prettier": 2 // Means error
    }
  }
  ' > .eslintrc.js
  ```
  > Make sure that plugin:prettier/recommended is the last configuration in the extends array
  
  The advantage of having prettier setup as an ESLint rule using eslint-plugin-prettier is that code can automatically be fixed using ESLint's --fix option.
  
  `.prettierrc`
  Create a *.prettierrc* configuration file for prettier in the **project root directory**. It can be either a JSON file or as *.prettierrc.js* a JavaScript file.
  
  ```shell
  echo '{
    "semi": true,
    "singleQuote": true
  }' > .prettierrc
  ```
  
  ### Add scripts to `package.json`
  In `package.json` under `scripts` add:
  ```javascript
  "scripts": {
    "start": "src/index.ts",
    "prettier": "prettier --config .prettierrc \\"src/**/*js\\" --write",
    "lint": "eslint \\"src/**/*.{js,ts,tsx}\\"",
    "build": "npx tsc"
  },
  ```
  - `npx` stands for Node Package Executer and comes with node
  - `npm run build` complies .ts files to .js files
  - `node .build/index.js` will run the application
  ## Add `GIT`
  #### Create a git repository for your project
  - run `git init`
  
  
  #### Create `.gitignore` file and add `node-modules`
  - run `echo 'node_modules' > .gitignore` in the terminal
  - as running `npm install` for any node project will install the dependencies defined in the `package.json` file a backup of those file are not needed
  
  #### Save you setup in your `git` repository
  - run `git add .`
  - run `git commit -m 'Initial Setup'`
  - add you remote git repositry with: `git remote add origin [remoteRepoURL]`
  - push to remote repository with: `git push origin master`
  
  
  #### Install lite-server
  - [GitHub - johnpapa/lite-server: Lightweight node server](https://github.com/johnpapa/lite-server)
  - lite server serves up the contents of the directory it's installed in. It will allow you to see your development as you do it
  - in the terminal run `npm install lite-server --save-dev`
  - it will create an `node_modules` directory and store all necessary files there 
  - it will add `lite-server` in `package.json` to `devDependencies` because of `--save-dev` (to store a true dependency add `--save`)
  - to make `lite-server` work:
    - modify the `"scripts"` in the projects `package.json`:
    - add `"start": "npm run lite",` to the beginning and `"lite": "lite-server"` at the end. (Don't forget to add commas where needed.)
    - this will ensure, that `npm start` with start by running the `lite-server`
  - to change the server port, watched file paths, and base directory for your project, create a `bs-config.json` in your project's folder:
  ```json
  {
    "port": 8000,
    "files": ["./src/**/*.{html,htm,css,js}"],
    "server": { "baseDir": "./src" }
  }
  ```
  - installing a node-module will create a `package-lock.json` file, which is a snapshot of all the dependencies of the project so far
  
  
  #### Start you node project
  - run `npm start`
  - based on the configured `package.json` file it will start you project by stargin the `lite-server`
  - the `lite-server` will serve the up the contents of the porject folder (the file, specified as `main` in the `package.json` file ?)  - it will also tell you in the terminal how to acces the served up content, on you local machine the default is `localhost:3000`
  - it will open you browser and serve up the files there
'''
linesHighlighted: [
  37
  57
  49
  89
]
isStarred: false
isTrashed: false
