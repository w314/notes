createdAt: "2021-05-02T18:44:03.759Z"
updatedAt: "2021-05-05T15:50:31.941Z"
type: "MARKDOWN_NOTE"
folder: "7869a5810e7871ff4be9"
title: "TypeScript"
tags: [
  "TypeScript"
]
content: '''
  # TypeScript
  - [TypeScript: Typed JavaScript at Any Scale.](https://www.typescriptlang.org/)
  - [TypeScript 4.0 Cheat Sheet \\| SitePen](https://www.sitepen.com/blog/typescript-cheat-sheet)
  - [TypeScript: Documentation - Do's and Don'ts](https://www.typescriptlang.org/docs/handbook/declaration-files/do-s-and-don-ts.html)
  
  ## Implicit Typing
  - TypeScript automatically assumes the types of objects
  - Best practice to use this when dealing with immutable variables and simple functions
  
  
  ## Explicit Typing
  ```typescript
  let myNumber: number;
  
  const squared = (num: number): number => {
    return num * num;
  };
  ```
  
  ### **Basic Types**:
  - string
  - number
  - boolean
  
  ### **Union Types**:
  Used when more than one type can be used
  ```typescript
  let phoneNumber: (number | string);
  
  // union with null
  const returnCapitalisedWord(word: string): string | null => {
    // returns word if word starts with capital letter, otherwise null
    const capitalWord = word.match(/[A-Z]/);
    return capitalWord;
  }
  
  // union with undefined (variable declared but not defined)
  const myFunc = (student: string | undefined) => {
    // does stuff 
  };
  ```
  
  ### **Other Types**:
  - void - used as return type, when function returns nothing
  - never - used as return type when function never returns anything like ones that throw errors or inifinite loops
  - any - DO NOT USE
  - unknown - used when type is unknown, used for type assertions
  
  ### Type Assertion
  ```typescript
  // using the "as" keyword
  const myVar = (req.query.param as unknown) as string;
  const myNum = ('15' as unknown) as number % 2;
  
  // using angle bracket notation
  const myVar = <string>(<unknown>req.query.param);
  ```
  
  ### Object-Like Types
  - arrays and tuples
    - tuples are not native to JavaScript
  ```typescript
  let arr1: string[];
  let arr2: (string | number)[];
  
  // or use a tuple
  let arr3: [number, string, string];
  ```
  - enum
    - enum is not native to JavaScript
    - use PascalCase with enum
  ```typescript
  // define enum
  enum Compass =  { North, South, East, West };
  
  // use enum as data type
  const move = (dist: number, direction: Compass) => {
    return 'walk ${dist} paces ${direction}';
  }
  ```
  
  ### Objects, Interfaces & Type Aliases
  If the object will never need additional properties later on you can: 
  ```typescript
  let student:{name: string, age: number, enrolled: boolean}  = 
  {
    name: 'Bob',
    age: 2,
    enrolled: true
  };
  ```
  **Better to use `interfaces`**:
  ```typescript
  interface Student {
    name: string;
    age: number;
    enrolled: boolean;
    phone?: number;
    readonly id: number;
  }
  
  interface PhdStudent extends Student {
    major: string;
  }
  ```
  - end lines with `;`
  - you can **add properties later** by declaring a new interface with extending on an earlier declared one
  - add `?` after property name if it's optional
  - `readonly` is a typescript construct it will only make typescript errors, there is no *readonly* in javascript. In JavaScript you can use `Object.freeze` if you want to make all properties of your object unmodifiable
  - `Duck Typing` is used by TypeScript for interfaces, it means that even though you say a function takes in an argument of interface type A, if interface type B has the same properties as A, it will also accept B. (If it walks like a duck and it quacks like a duck...)
  - use *PascalCase* for interface names
  
  **Type Aliases**
  Type Aliases do not create a new type they rename an already existent one.
  ```typescript
  type Name: string;
  type Input: string | number;
  type Coord: [numer, number];
  ```
  
  Type Aliases can also by used for objects.
  [TypeScript: Documentation - Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)
  Type aliases for objects and interfaces are very similar, and in many cases you can choose between them freely. Almost all features of an `interface` are available in `type`, the key distinction is that a type cannot be re-opened to add new properties vs an interface which is always extendable.
  
  - Extending an interface / type
  ```typescript 
  // Extending an Interface
  
  interface Animal {
    name: string
  }
  
  interface Bear extends Animal {
    honey: boolean
  }
  
  const bear = getBear() 
  bear.name
  bear.honey
          
  // Extending a type via intersections
  
  type Animal = {
    name: string
  }
  
  type Bear = Animal & { 
    honey: Boolean 
  }
  
  const bear = getBear();
  bear.name;
  bear.honey;
  ```
  
  - Adding new fields to an existing interface
  ```typescript
  // Adding new field to an exisitng interface
  interface Window {
    title: string
  }
  
  interface Window {
    ts: TypeScriptAPI
  }
  
  const src = 'const a = "Hello World"';
  window.ts.transpileModule(src, {});
          
  // A type cannot be changed after being created
  
  type Window = {
    title: string
  }
  
  type Window = {
    ts: TypeScriptAPI
  }
  
   // Error: Duplicate identifier 'Window'.
  ```
  
  **Using interfaces for `Factory Functions`**
  Factory functions are functions that are returning objects.
  ```typescript
  interface Student {
    name: string;
    age: number;
    greet(): void;
  }
  
  const studentFactory = (name: string, age: number): Student =>{ 
    const greet = ():void => console.log('hello'); 
    return { name, age, greet };
  }
  
  const myStudent = studentFactory('Hana', 16);
  
  ```
  ### Classes
  - can use access modifiers
    - `public` by default all properties of TypeScript classes are public
    - `private` (or `#`) properties can only be accesssed  and modified within the class itself. Using it only will give you a typescript error, there are no true private variables in JavaScript
    - `protected` can only be accessed by the class and its deriving classes. If *Person* has *name* and *Employee* extends *Person*, we can use *name* within *Employee* class but not outside of it.
  ```typescript
  class Person {
    protected name: string;
    constructor(name: string) {
      this.name = name;
    }
  }
  
  class Employee extends Person {
    private department: string;
  
    constructor(name: string, department: string) {
      super(name);
      this.department = department;
    }
  
    public getElevatorPitch() {
      return `Hello, my name is ${this.name} and I work in ${this.department}.`;
    }
  }
  
  let howard = new Employee("Howard", "Sales");
  console.log(howard.getElevatorPitch());
  console.log(howard.name);
  // Property 'name' is protected and only accessible within class 'Person' and its subclasses.
  ```
  
  ### Generics
  ```typescript
  // Typed Function
  const getItem = (arr: number[]):number => {
    return arr[1];
  }
  
  // Generic Function
  const getItem = <T>(arr: T[]):T => {
    return arr[1];
  };
  
  
  // regular typescipt
  let arr = number[];
  // with Generics
  let arr = Array<number>;
  ```
  In case of the generic function, we can use it with numbers as well as string. Whatever type will call the function will translate to its return as well.
  
  
  
  
  
  
'''
linesHighlighted: [
  15
  7
  119
]
isStarred: false
isTrashed: false
