createdAt: "2021-07-07T17:00:05.749Z"
updatedAt: "2021-10-15T21:19:34.278Z"
type: "MARKDOWN_NOTE"
folder: "7b7225fb954665754643"
title: "Node Express Jasmine TypeScript ESLint Prettier"
tags: [
  "node"
  "express"
  "jasmine"
  "typescript"
  "eslint"
  "prettier"
]
content: '''
  # Node Express Jasmine TypeScript ESLint Prettier
  
  ## Setup new project by cloning projectBase
  ### Clone projectBase repository
  ```shell
  git clone https://github.com/w314/projectBase.git <newProjecName>
  ```
  ### Start App
  - install dependecies
  ```shell
  npm install
  ```
  - start your app
  This will run the app from the `index.ts` file under the `src` directory.
  
  ```shell
  npm start
  ```
  
  The following scripts should run without error
    - `npm run prettier`
    - `npm run lint`
    - `npm start`
    will run the app from the starting page under *src* folder
    - `npm run build`
    will convert typescript to javascript and create the *dist* distribution folder
    - `npm run test`
    builds app and runs jasmin to test if *localhost:3000/api/sampleRoute* displays the text *Application starting page*
    - `node index.js` 
    will run the app from the *index.js* file under the *dist* directory, to use it you have to run *npm build* first to create the *dist* directory
  
  ## Setup GIT
  
  - create remote repository for you new project and replace the remote to point to this new repository
  ```shell
  git remote remove origin
  ```
  ```shell
  git remote add <newProjectRemoteRepo>
  ```
  - setting up the project won't make any changes but, if you made any other changes, make your initial commit
  ```shell
  git add .
  git commit -m 'feat: Initial commit'
  
  ```
  Otherwise push your local repository to remote:
  ```shell
  git push origin master
  ```
  
  
  ## Setup Node Project Locally
  ### setup file structure and intiate node project
  ```shell
  #CREATE PROJECT DIRECTORY
  # create project directory
  mkdir projectBase
  # go to project directory
  cd projectBase
  # add readme file
  touch README.md
  
  #INITIATE NODE PROJECT
  npm init -y
  
  # SETUP PRETTIER
  # install prettier
  npm i --save-dev prettier eslint-config-prettier eslint-plugin-prettier
  # add configuration file
  echo '{
    "semi": true,
    "singleQuote": true
  }' > .prettierrc
  
  # SETUP ESLINT
  # install eslint
  npm i --save-dev eslint @typescript-eslint/parser @typescript-eslint/eslint-plugin
  # add configuration file
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
      "no-console": "off",
      "prettier/prettier": 2 // Means error
    }
  }
  ' > .eslintrc
  
  # SETUP TYPESCRIPT
  # create src directory for typescript files
  mkdir src
  # install typescript
  npm i --save-dev typescript ts-node @types/node
  # create typescript config file (needs typescript installed)
  npx tsc --init
  
  
  # SETUP JASMINE
  
  # install jasmine
  npm i jasmine jasmine-spec-reporter
  
  # install type definitions for jasmine
  npm i --save-dev @types/jasmine
  
  
  # create file structure for testing
  mkdir spec
  mkdir spec/support
  echo '{
    "spec_dir": "dist/tests",
    "spec_files":  [
        "**/*[sS]pec.js"
    ],
    "helpers": [
      "helpers/**/*.js"
    ],
    "stopSpecOnExpectationFailure": false,
    "random": false 
  }' > spec/support/jasmine.json
  mkdir src/tests
  mkdir src/tests/helpers
  echo "import { DisplayProcessor, SpecReporter, StacktraceOption } from 'jasmine-spec-reporter'
  import SuiteInfo = jasmine.SuiteInfo
  
  class CustomProcessor extends DisplayProcessor {
    public displayJasmineStarted(info: SuiteInfo, log: string): string {
      return `TypeScript ${log}`
    }
  }
  
  jasmine.getEnv().clearReporters()
  jasmine.getEnv().addReporter(
    new SpecReporter({
      spec: {
        displayStacktrace: StacktraceOption.NONE,
      },
      customProcessors: [CustomProcessor],
    })
  )" > src/tests/helpers/reporter.ts
  # create spec file for index.js
  touch src/tests/indexSpec.ts
  
  # install supertest and its types for HTTP server testing
  npm i --save-dev supertest @types/supertest
  
  # add spec file to test index.js
  echo "import { agent as request } from 'supertest';
  import app from '../index';
  
  //test api/sampleRoute endpoint
  describe('GET api/sampleRoute', () => {
    it('responds with: Application starting page', (done) => {
      request(app)
        .get('/api/sampleRoute')
        .expect(200)
        .expect('Content-Type', 'text/html; charset=utf-8')
        .then((response) => {
          expect(response.text).toBe('Application starting page');
          done();
        })
        .catch((Error) => {
          Error ? done.fail(Error) : done();
        });
    });
  });
  " > src/tests/indexSpec.ts
  
  # SETUP EXPRESS
  
  # install express
  npm i express
  
  # install type definitions and nodemon (nodemon restarts server after each save)
  npm i --save-dev @types/express nodemon
  
  # setup routing file structure
  mkdir src/routes
  
  # create main router file
  echo "import express from 'express'
  //import your routes
  import sampleRoute from './api/sampleRoute'
  
  //create router object
  const routes = express.Router();
  
  //set up router object to use your routes
  routes.use('/sampleRoute', sampleRoute); 
  
  //export router object
  export default routes;
  " > src/routes/index.ts
  
  # create directory for routes
  mkdir src/routes/api
  
  # create sample route page
  echo "import express from 'express'
  
  //create router object
  const sampleRoute = express.Router();
  
  //set up route
  sampleRoute.get('/', (req, res) => {
      res.send('Application starting page');
  });
  
  //export route
  export default sampleRoute;
  " > src/routes/api/sampleRoute.ts
  mkdir src/routes/utilities
  
  
  # ADD PROJECT STARTING FILE
  
  echo "import express from 'express'
  //import routes
  import routes from './routes/index'
  
  //create the server and set the port
  const app = express();
  const port = 3000;
  
  //setup your app to use the router
  app.use('./api', routes);
  
  //start the server
  app.listen(port, () => {
    console.log(`Server started at http://localhost:\\${port}/api/sampleRoute`);
  });
  
  export default app;
  " >  ./src/index.ts
  
  ```
  
  ### edit typescript configuration file
  The **npx tsc --init** command created the **tsconfig.json** configuration file for typescript.
  Make sure that the following settings are set correctly
  Had to update the lines:
    - lib
    - outdir
    - noImplicitAny
    - esModuleInterop
    */node_modules/@types/express/index"' can only be default-imported using the 'esModuleInterop' flag*
  
    - add exclude line
  ```javascript
  {
    "compilerOptions": {
      "target": "es5",                          
      "module": "commonjs",                     
      "lib": ["ES2018", "DOM"], 
      "outDir": "./dist",                        
      "strict": true,                           
      "noImplicitAny": true,     
      "esModuleInterop": true,
    },
    "exclude": ["node_modules", "dist", "spec"]
  }
  ```
    
  ### edit package.json
  Edit the `scripts` in `package.json` to include these scripts:
  
  ```javascript
  "scripts": {
      "start": "nodemon src/index.ts",
      "prettier": "prettier --config .prettierrc \\"src/**/*{js,ts,tsx}\\" --write",
      "lint": "eslint \\"src/**/*.{js,ts}\\"",
      "build": "npx tsc",
      "jasmine": "jasmine",
      "test": "npm run build && npm run jasmine"
  },
  ```
  
  ### add git
  ```shell
  git init
  touch "node_modules" > .gitignore
  
  ```
  
  - setup remote repository
  After creating repository in github add it as remote, and make your initial commit.
  ```shell
  git remote add origin <remote_repo>
  ```
  ```shell
  git add .
  ```
  ```shell
  git commit -m "feat: Initial commit"
  git push origin master
  
  ```
  
  
'''
linesHighlighted: [
  111
  120
  227
  158
]
isStarred: false
isTrashed: false
