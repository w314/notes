createdAt: "2021-05-05T15:03:39.925Z"
updatedAt: "2021-07-09T16:46:16.772Z"
type: "MARKDOWN_NOTE"
folder: "7b7225fb954665754643"
title: "Jasmine"
tags: [
  "test"
  "jasmin"
]
content: '''
  # Jasmine
  [Jasmine Documentation](https://jasmine.github.io/index.html)x
  
  ## Setup Jasmine for Node project
  
  Server side Jasmin tests the compiled JavaScript code, and cannot test the TypeScript code.
  
   ### installation
   ```bash
   npm i jasmine jasmine-spec-reporter
  ```
   - **jasmine-spec-reporter** is an app that makes reporting in terminal easier to read
  ```bash
  npm i --save-dev @types/jasmine
  ```
  - types for TypeScript
  
  ### add to `packages.json` under `scripts`
  Remember, jasmine tests JavaScript files not TypeScipt, so you have to build your project before testing.
  ```bash
  "jasmine": "jasmine",
  "test": "npm run build && npm run jasmine"
  ```
  
  ### setup file structure & configuration
  ```bash
  mkdir spec
  mkdir spec/support
  touch spec/jasmine.json
  mkdir src/tests
  touch src/tests/indexScpec.ts
  mkdir src/tests/helpers
  touch src/tests/helpers/reporter.ts
  
  ```
  - as we are testing compiled javascript code, our test need to end up in the *dist (build)* folder where our final javascript code end. Therefore we create our `tests` folder under the *src* folder
  - `indexSpec.ts` will test our main index file
  **jasmine.json** under *spec* will hold the primary configuration for jasmine
  ```javascript
  {
    "spec-dir": "dist/tests",
    "spec-files":  [
        "**/*[sS]pec.js"
    ],
    "helpers": [
      "helpers/**/*.js"
    ],
    "stopSpecOnExpectationFailure": false,
    "random": false 
  }
  ```
  
  **reporter.ts**  under *tests/helpers* will be the primary configuration file for the spec reporter
  
  As per `jasmine-spec-reporter` documentation:
  [Configuration for using jasmine-spec-reporter with TypeScript](https://github.com/bcaudan/jasmine-spec-reporter/tree/673e22cd3b13732b421a25e862dbe887692ed345/examples/typescript)
  ```typescript
  import { DisplayProcessor, SpecReporter, StacktraceOption } from 'jasmine-spec-reporter'
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
  )
  ```
  **tsconfig.json**:  add the "spec" directory to exludes.
  ```bash
  ,
    "exclude": ["node_modules", "./dist", "spec"]
  ```
  
  ## Write test scripts
  - match the name of test scripts to the name of files tested by adding `Spec` to end of the name of the file
  
  My index.ts file:
  ```typescript
  const myFunc = (num: number): number => {
    return num * num;
  };
  
  export default myFunc;
  ```
  
  - My test file:
  ```bash
  touch src/tests/indexSpec.ts
  ```
  - `Suite` is a collection of similar tests related to  one function
  - `Specs` are the individual tests
  ```typescript
  // import function to test first
  import myFunc from "../index";
  
  // describe suite to test
  describe('testing index file', () => {
    // add specs test the suite
    it('expect myFunc(5) to equal 25', () => {
      expect(myFunc(5)).toEqual(25);
    });
  });
  ```
  I can run my test script with `npm run test`.
  
  
  ### testing asynchronous code
  - with async/await
  ```typescript
  it('expects asyncFunc() result to equal value', 
    async () => {
      const result = await asyncFunc();
      expects(result).toEqual(value);
  
  });
  ```
  - with using promise syntax
  ```typescript
  it('expects  asyncFunc() result to equal value', 
    () => {
      return asyncFunc().then( result => {
      expect(result).toEqual(value);
    });
  )};
  ```
  Testing Promise resolution / rejection can be done with Jasmine ES6 Promise Matchers Library (https://www.npmjs.com/package/jasmine-es6-promise-matchers)
  - `.toBeResolved()`
  - `.toBeRejected()`
  - `.toBeRejectedWith(expected value)`
  
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
