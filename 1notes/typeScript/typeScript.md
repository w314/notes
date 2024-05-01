# TypeScript

- Superset of JavaScript. 
- transpiled into JavaSrcipt with `tsc myFile.ts`
- open source
- strongly typed: must declare variable type at declaration
- strictly typed: no implicit type coersion


### Transpilation
Transforms source code written in one language (eg. TypeScript) to another language (eg. JavaScript) with a similar level of abstraction.

## TypeScript Data Types

### any

### arrays

### union types

### enums
#### string enums
#### numeric enums

### never & void

## Classes

## Interfaces

## Functions

## Decorators

## Generics

## Casting
```ts
let x: unknown = 'hello';

// casting with `as`
console.log((x as string).length);

// casting using <>
console.log((<string>x).length);
```


## Keyof
Keyof operator takes an object type and produces a string or numeric literal union of its keys.

It can be used that a string is valid key on the object or not

```ts
interface Person {
  name: string;
  age: number;
}

keyof Person // results in  "name" | "age"
````

## Utility Types

## Type Guards

## TypeScript Configuration



