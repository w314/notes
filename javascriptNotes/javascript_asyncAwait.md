createdAt: "2020-11-20T21:44:59.476Z"
updatedAt: "2020-11-21T16:11:23.721Z"
type: "MARKDOWN_NOTE"
folder: "7869a5810e7871ff4be9"
title: "JavaScript Async/Await"
tags: []
content: '''
  js, javascript, async, await
  # JavaScript Async/Await
  
  - [Asynchronous JavaScript: Async/Await Tutorial \\| Toptal](https://www.toptal.com/javascript/asynchronous-javascript-async-await-tutorial)
  - [Making asynchronous programming easier with async and await - Learn web development \\| MDN](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Async_await)
  
  
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
  
  
  
'''
linesHighlighted: []
isStarred: false
isTrashed: false
