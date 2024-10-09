# JS Quizes

What is the output?
```js
function call() {  
    var obj = { prop1: function () { return this.prop2; }, prop2: 1 }  
     console.log(typeof obj.prop1());  
}   
call();
```

-> number : 
obj.prop1 will have the value of prop2

<hr>


What is the output?

```js
function foo() {
    console.log("Inside Foo");
    return bar;
}

function bar() {
    console.log("Inside Bar");
    return test;
}

function test(){
    console.log("Inside Test");
}
foo()()();
```
-> Inside Foo Inside Bar Inside Test