java, oop, instance-variables, &&, 

## Variables

- local variables have to be initialized
- using uninitialized local variables results compile error

- for `Byte`, `Short`, `Integer`, `Long` varaibles values -128-127 are cashed like strings in the String Pool

## Operators
- when using `exp1 && exp2` if `exp1` is false `exp2` never gets evaluated

What is the output of this code?
```java
public class Question {
    public static void main(String[] args) {
        String a = "xy";
        String b = "xyz";
        System.out.println(a = b);
    }
}
```
`xyz` the assignment happens first and the value `a` is displayed


## Arrays
What are valid ways to declare an array?
```java
// 1
int myArr1[3];
// 2
int myArr2[];
// 3
int myArr3[] = new int[3];
// 4
int myArr4[3] = new int[3];
// 5
int[] myArr5 = new int[3];
// 6
int myArr6 = new int[];
// 7
int myArr7 = null;
```
Valid: 2, 3, 5, 7
Invalid 1, 4, 6
## OOP
- during object creation instance variables are automatically assigned default values (unlike local variables that have to be initialized)

- `this()` can be used to invoke the constructor of the current class


### Polymorphism

` Bike hondaBike = new Honda()`
- when invoking methods Honda class methods will be used
- when accessing variables, Bike class variables will be used



## Inheritance
- private member of a class (methods, variables) while inherited are NOT accessible, visible to the child class

## Interface

- interface A extends interface B
- class A extends class B
- class A implements interface B


