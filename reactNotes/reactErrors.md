react, problems, error, strict-mode

# React Problmes

## [Strict mode will call reducer functions twice](https://stackoverflow.com/questions/54892403/usereducer-action-dispatched-twice)
With a simple add to cart function it will add the same item is added twice.
Strict mode does it to make sure our functions are pure.
In this case I've updated the function to edit the quantity if productId was already in cart.

## Not Found - GET https://registry.npmjs.org/cra-template-typescrpipt - Not found

- uninstall global create-react-app with `npm uninstall -g create-react-app`
- run npx create-react-app.... again

