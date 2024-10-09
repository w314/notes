  js, javascript, promises
  
  # JavaScript Promises
  > Promise is a holder for a result (or error) that will become availabe in the future.

  - replaced callback in async javascript programming
  - the `Promise Object` represents the eventual completion (or failure) of the async operation and its resulting value
  - callbacks can be attached to the returned promise object instead of passing them to a function

## Promise Syntax

```js
let myPromise = new Promise(function(resolve, reject)) {
    // async code
    // resolve is if success
    // reject if failure
};
```
- the constructor of the promise accepts only one argument:  a function
- this function has two arguments:
    - resolve
    - reject

## States of Promises

A Promise has three states:
- pending
- resolved
- rejected

## Handling a Promise

```js
var myPromise = new Promise(function (resolve, reject) {
	setTimeout(function () {
		resolve("success");
	}, 2000);
});

myPromise.then(
	function (data) {
		console.log(data + " received in 2 seconds");
	},
	function (error) {
		console.log(error);
	}
);

// to make it run put then directly after promise like
//  new Promise(...).then(...)
```

## Error Handling in Promises

```js
asyncFunction()
    .then(  )
    .catch(  )
    .finally(  )
```
  
## Handle several promises

### `Promise.allSettled`
  - returns a promise
  
  ```javascript
  const book1 = new Promise((resolve, reject) => {
      setTimeout(resolve, 3000, "Enders Game");
  });
  
  const book2 = new Promise((resolve, reject) => {
      setTimeout(reject, 4000, "Sorry, not available!");
  });
  
  const book3 = new Promise((resolve, reject) => {
      setTimeout(resolve, 2000, "Harry Potter and The Prisoner of Azkaban");
  });
  
  const book4 = new Promise((resolve, reject) => {
      setTimeout(resolve, 1000, "Stranger in a Strange Land");
  });
  
  Promise.allSettled([book1, book2, book3, book4])
  .then(results => {
      console.log(results)
      results.forEach(result => console.log(result.value))
  })
  .catch(error => console.log(error));
  ```

  ## ThinkOvers

  What is the output?
  ```js
  new Promise(function (resolve, reject) {
	let b;
	setTimeout(compute = (a) => resolve(a + b), 10000);
	b = 25;
}).then(function (data) { console.log(data); });
compute(5);
```
- output is: 30
- a equals 5
- b = 25 will be executed before the setTimeOut function


## Literature
  
  - [Graceful asynchronous programming with Promises - Learn web development \\| MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Promises)
  - [Promisees · Courtesy of ponyfoo.com](http://bevacqua.github.io/promisees/)
  - [JavaScript: Learn Promises. JavaScript Promises made easy. Learn… \\| by Brandon Morelli | codeburst](https://codeburst.io/javascript-learn-promises-f1eaa00c5461)
  - [Error handling in long Promise chains \\| by Arthur Xavier | Medium](https://medium.com/@arthurxavier/error-handling-in-long-promise-chains-155f610b5bc6)
  