createdAt: "2020-02-20T18:10:14.177Z"
updatedAt: "2020-02-21T21:09:24.027Z"
type: "MARKDOWN_NOTE"
folder: "0502aa55141f2315e808"
title: "Mocha for Testing"
tags: [
  "unit_testing"
  "testing"
  "mocha"
]
content: '''
  # `Mocha` for Testing
  
  `Testing environment` is the place where you run your tests, like `node.js`or the  browser.
  `Testing frameworks` are used to create, organize and execute tests, like `Mocha` or `Jasmin`.
  `Assertion libraries` are tools to verify that things are correct, like `chai.js`, `Node.js` `assert` module. They verify your test results, saving you lots of `if` statements.
  
  ```js
  //Example using should.js and Node.js assert module
  var output = mycode.doSomething();
  output.should.equal('bacon'); //should.js
  assert.eq(output, 'bacon'); //node.js assert
  
  // The alternative being:
  var output = mycode.doSomething();
  if (output !== 'bacon') {
    throw new Error('expected output to be "bacon", got '+output);
  }
  ```
  
  ## Unit testing with `Mocha` in `Node`
  
  [Mocha](https://github.com/mochajs/mocha.git) is a javascript test framework running in `Node.js` and in the browser.
  
  ## Setup `Mocha`
  - install by running
  `npm install --save-dev mocha`
  
  - edit `"test:"` under `"scripts" ` in the `package.json` file
  - run tests with
  `npm run test`
  
  ## Mocha tests
  
  Considering you have a divide function in a units.ts file:
  ```js
  export const divide = (a: number, b: number) => {
      if(b === 0) { throw new Error('div by 0') }
  
      return a / b;
      }
  ```
  You write your test in a units.tests.ts file
  ```js
  import { divide } from './units';
  import { expect } from 'chai';
  import 'mocha';
  
  describe('divide', () => {
  
    it('should divide 6 by 3', () => {
      const result = divide(6,3);
      expect(result).to.equal(2);
    });
  
    it('should divide 5 and 2', () => {
      const result = divide(5,2);
      expect(result).to.equal(2.5);
    });
  
    it('should throw an error if div by zero', () => {
      expect(()=>{ divide(5,0) }).to.throw('div by 0')
    });
  
  });
  ```
  
  In you `package.json` you have:
  `"test": "mocha -r ts-node/register yourTestPath/*.tests.ts"`
  
  You'll run you test in the terminal with:
  `npm run test`
'''
linesHighlighted: []
isStarred: false
isTrashed: false
