## What is the advantage of using React as opposed to using plain Javascript
## Tell me about the virtual DOM.

## What is TSX? (they may ask about JSX, just remind them we used React Typescript and TSX, not JSX)
- tsx = typescript xml
- view rendering syntax of react

What are components in React?
How do you create a component in React?
What is "export" in React?
What is props and state?
Can you send props from child to parent?
How does Routing work in React? How did you you create routes?
What is the component lifecycle in react? (class component question, don't worry about it)
Describe the function component hooks you've used

## What is axios? What have you used it for?
 - promise-based HTTP client
 - way to make API requests
 - returns a promise


 Promise returned resolves to an object containing:

- data: the response body from the server.
- status: the HTTP status code from the server response.
- statusText: the HTTP status message from the server response.
- headers: all the headers that the server responded with.
- config: the original request configuration.
- request: the request that generated this response. 
 

 ```js
axios.get('/user?ID=12345')
  .then(function (response) {
    // handle success
    console.log(response);
  })
  .catch(function (error) {
    // handle error
    console.log(error);
  })
  .finally(function () {
    // always executed
  });

// or using async-await
async function getUser() {
  try {
    const response = await axios.get('/user?ID=12345');
    console.log(response);
  } catch (error) {
    console.error(error);
  }
}
 ```
  
## How can I render a list of elements in React?
## How can I conditionally render content in React?