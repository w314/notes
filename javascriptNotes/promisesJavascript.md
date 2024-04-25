  js, javascript, promises
  
  # JavaScript Promises
  
  ### About Promises:
  
  - [Graceful asynchronous programming with Promises - Learn web development \\| MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Promises)
  - [Promisees · Courtesy of ponyfoo.com](http://bevacqua.github.io/promisees/)
  - [JavaScript: Learn Promises. JavaScript Promises made easy. Learn… \\| by Brandon Morelli | codeburst](https://codeburst.io/javascript-learn-promises-f1eaa00c5461)
  - [Error handling in long Promise chains \\| by Arthur Xavier | Medium](https://medium.com/@arthurxavier/error-handling-in-long-promise-chains-155f610b5bc6)
  
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