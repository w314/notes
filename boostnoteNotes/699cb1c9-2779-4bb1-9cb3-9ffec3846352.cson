createdAt: "2021-01-18T17:15:21.322Z"
updatedAt: "2021-03-10T14:41:16.398Z"
type: "MARKDOWN_NOTE"
folder: "bb83f5f87373282090b3"
title: "C++ Functions"
tags: [
  "class"
  "name_space"
  "polymorpishm"
  "overloading"
  "overriding"
  "hiding"
]
content: '''
  # C++ Functions
  
  ## passing by reference with `&`
  
  ```c
  #include <iostream>
  #inlcue <vector>
  using std::cout;
  using std::vector;
  
  // `&` makes passing by reference
  int AdditionalFunction(const vector<int> &v) {
    int sum = 0;
    // by declaring &i we don't make copies of
    // the values of v just pass them by reference
    for(const int &i : v) {
      sum += i;
    }
    return sum;
  }
  ```
  
  `name spaces` allow us to group logically related variables and functions together. They also help to avoid conflicts between variables of the same name.
  
  ```c
  namespace English {
  void Hello() { std::cout << "Hello, World!\\n"; }
  }  // namespace English
  
  namespace Spanish {
  void Hello() { std::cout << "Hola, Mundo!\\n"; }
  }  // namespace Spanish
  
  int main() {
    English::Hello();
    Spanish::Hello();
  }
  ```
  
  ### Standard Library
  `std` is the `namespace` used by the `C++ Standard Library`
  
  ## Polymorphism
  In the context of object oriented programming `polymorpishm` describes a paradigm in which a function may behave differently depending on how it's called. Polymorphism can be achieved in two ways in c++:
  - overloading
  - overriding
  
  ## overloading
  Define function with different input parameters.
  ```c++
  #include <cassert>
  #include <string>
  
  // creating empty classes
  // compiler will create default constructors
  class Water {};
  class Alcohol {};
  
  class Human {
  public:
      std::string condition{"happy"};
      void Drink(Water water) { condition = "hydrated"; }
      void Drink(Alcohol alcohol) { condition = "impared"; }
  };
  
  int main() {
      Human bob;
      assert(bob.condition == "happy");
      // using default constructor to pass Water object
      // as we gave it no name it's an anonymus object
      bob.Drink(Water());
      assert(bob.condition == "hydrated");
      bob.Drink(Alcohol());
      assert(bob.condition == "impared");
  }
  ```
  
  ## overriding
   - Derived classes can override functions of base classes.
   - if the base class function is `virtual` it is called `overriding`
   - if it not virtual the process called `hiding` 
  ### Virtual Functions
  - `Virtual functions` are a polymorphic feature.
  - They allow us to define an `abstract class` that can act as an `interface` from which other classes can be derived.
  - A `pure virtual` function is a virtual function that the base class declares but does not define. Appending `= 0` to the function declares them to be "pure" virtual functions. `= 0` means the function is declared but not defined.
  - A pure virtual function makes a class `abstract` , it means it cannot be instantiated, only classes derived from the abstract class which override the pure virtual function can be instantiated.
  ```c
  #include <iostream>
  
  class Animal {
      // virtual means derived classes can override it
      // "= 0" makes it a pure virtual function
      // this will make it an abstract class with no instances
      // it will function as an interface where all derived classes 
      // will inherit and have to implement this funciton
      virtual void Talk() const = 0;
  };
  
  class Human : public Animal {
  public:
      // "override" keyword is not necessary, but good practice
      // to show the compiler and others it is an override
      void Talk() const override {
        std::cout << "Hello!\\n";
      }
  };
  
  int main() {
      Human human;
      human.Talk();
      // if we would try to create an Animal animal
      // would get error message: 
      // cannot declare variable 'animal' to be of abstract type 'Animal'
      // because the following virtual functions are pure within 'Animal': Talk()
      // Animal animal;
  }
  ```
'''
linesHighlighted: [
  68
  80
]
isStarred: false
isTrashed: false
