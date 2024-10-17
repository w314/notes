# JS Modules

- each module is a JavaScript file
- help to isolate state and global namespace
- enable reusability
- help maintainablity
- by default modules are in strict-mode code
    - => means scope of the members are always local
        - funtions
        - variables
        - etc
    - functions and variables are only visible outside if explicitely exported
- modules are declarative in nature
    - use `export` to export any variable/method/object
    - use `import` to consume an other's module exported variables

## Creating Moduls

### Exports

Type of exorts
- Named Exports
    - more per module
    - recognized by their name
```js
// export individual features
export let myVar; // works also with const, var
export funtion myFunction() {}

// export list
export { myVar, myFunction};
```

- Default Exports
    - one per module
    - used for the most highly used entity
    - a module can have BOTH named and a default export

```js
// has to be used with directly with the function declaration
export default sayHi() { console.log('hi'); }

// OR
const sayHello = () => console.log('hello');
export default sayHello;
```


### Imports
A module can have as many imports as needed.

```js
// import multiple export form a module
import { entity1, entity2 } from './otherModule.js';

// import entire module's content
// must declare name for object with as objectName
import * as nameForObject from './otherModule.js';

// use alias for convenience
import { enitityName as betterName } from './otherModule.js';

// you can import a default export with any name
import myNameForYourDefaultExport from './otherModule.js';
```

## Errors & Solution

### Cannot use import statement outside a module



