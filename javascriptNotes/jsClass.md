classes

# Class

```js
class Person {

    // constructor
    constructor(name, age) {
        this.name = name;
        this.age = age;
    }

    // method
    greet() {
        console.log("hi");
    }

    // static method
    rights() {
        console.log("Person has human rights")
    }
}


let bob = new Person("bob", 3);

// call static method
Person.rights();


```
## Inheritance
- uses `extends` keyword
- subclass inherits all methods static or non-static
- `super` keyword is used to refer to the parent class's methods/constructors
- built-in classes can also be extended

```js
class Child extends Person {

    constructor(name, age, favToy) {
        super(name, age);
        this.favToy = favToy;
    }
}
```
