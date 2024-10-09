# Fetch API
> Provides a way to communicate with the server. Send requests, receive responses.

## Basic Syntax

```js
PromisReturned = fetch(url, [options])
```
- returns a promise
- without options makes a simple GET request


## Getting Response from Fetch

1. resolve promise returned by fetch to an object
2. get body/data from response object
    - `response.text()`  as text
    - `response.json()`  as JSON
    - `response.formData()` as FormData
    - `response.blob()` as blob (binary data with its type)

```js
let response = await fetch(url);
// if HTTP status is 200-299
if( response.ok ) {
    // get response body
    let json = response.json();
} else {
    console.log('HTTP-Error: ' + response.status);
}

```
`response.blob()` returns the response body as binary object