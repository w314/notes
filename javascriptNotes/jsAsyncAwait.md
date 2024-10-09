
# JavaScript Async/Await
  
## Async Function

- declared with the `async` keyword
- always returns a `promise`

  
  ```javascript
  const mockAPI = (returnValue) => (arg, cb) => {
      setTimeout(() => cb(returnValue), 2000);
  };
  
  const fetchSession = mockAPI({ id: "123765" });
  const fetchUser = mockAPI({ firstname: "Bob" });
  const fetchUserFavorites = mockAPI([ "lions", "tigers", "bears" ]);
  
  const runAsync = async () => {
      try {
          const session = await fetchSession("session-id");
          const user = await fetchUser(session);
          const favorites = await fetchUserFavorites(user);
          console.log(favorites);
      } catch (error) {
          console.log("oops!");
      }
  }
  ```

  ## Literature
    
- [Asynchronous JavaScript: Async/Await Tutorial](https://www.toptal.com/javascript/asynchronous-javascript-async-await-tutorial)
- [Making asynchronous programming easier with async and await - Learn web development \\| MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await)
 