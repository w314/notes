createdAt: "2021-02-03T21:21:00.753Z"
updatedAt: "2021-03-10T17:51:05.457Z"
type: "MARKDOWN_NOTE"
folder: "bb83f5f87373282090b3"
title: "C++ Classes"
tags: [
  "class"
  "scope_resolution"
  "scope"
  "initalization"
  "initializer_list"
  "encapsulation"
  "mutator"
  "abstraction"
  "inheritance"
  "composition"
  "friend_class"
]
content: '''
  # C++ Classes
  
  - by default all member of classes are private
  
  ```c
  class Date {
    public:
      int Day() { return day; }
      void Day(int d) {
        if (d >= 1 && d <= 31) day_ = d;
      }
    private:
      int day_{1};
      int month_{1};
      int year_{0};
  };
  ```
  
  `encapsulation`: we bundle related properties together in a single class
  `abstraction`: users of our class only need to be familiar with the interface we provide
  `constructor`: we use them instantiate objects, functions that constract objects of a class
  -  all classes come with default constructors that take no argument
  -  we can define our own constructor and there can be mutliple different ways to instantiate objects of the class
  -  *an operation that initializes (“constructs”) an object. Typically a constructor establishes an invariant and often acquires resources needed for an object to be used (which are then typically released by a destructor).*
  
  ```c
  class Date {
    public:
      // constructor, uses name of the class
      Date(int d, int m, int y) {
        // calls mutator functions
        Day(d);
      }
      int Day() { return day; }
      void Day(int d) {
        if (d >= 1 && d <= 31) day_ = d;
      }
    private:
      int day_{1};
      int month_{1};
      int year_{0};
  };
  
  
  
  ```
  
  `scope resolution` allows us to tell the compiler what scope a particular identifier is assosiated with.
  `scope resulion operator` is `::`
  
  
  #### separating the declaration and definition of the compiler
  
  ```c
  class Date {
  public:
    //declare the compiler
    Date(int d, int m, int y);
    // declare functions
    void Day(int day);
  }
  
  // define the compiler outside of class definition
  // we use scope definition to connect the constructor to the class
  Date::Date(int d, int m, int y) {
    Day(d);
    Month(m);
    Year(y);  
  }
  
  // define Day() functions
  void Date::Day(int day) {
    if (day >= 1 && day <= 31) {
      Date::day = day;
    }
  }
   
  ```
  
  ## Initializer Lists
  `Initializer lists` initialize member variables to specific values just before a the class constructor runs. This intitialization ensures that class members are automatically initialized when an instance of the class is created. Before even the constructor itself runs and the object itself is created.
  - prefer initialization to assigment
  - assignment creates an opportunity to accidentally use a variable before its value is set
  - member variables initialized through an intitialization list can be declared `const`, but not those initialized within the body of the constructor
  
  ```c
  // year is initialized through an initialization list
  // as the value of day and month are checked we call their mutator functions
  Date::Date(int d, int m, int y) : year(y) {
    Day(d);
    Month(d);
  }
  ```
  
  Other initialization example:
  ```c
  #include <assert.h>
  #include <string>
  
  // using struct as everything is public 
  struct Person {
  struct Person {
  public:
    // Define a public constructor with an initialization list
    Person(std::string const & n) : name(n) {}
    std::string const name;
  };
  
  // Test
  int main() {
    Person alice("Alice");
    Person bob("Bob");
    assert(alice.name != bob.name);
  }
  ```
  
  `encapsulaton` is the grouping together of data and logic into a single unit. In object-oriented programming classes encapsulate data and functions that opeate on the data.
  
  
  `const` member functions
  member functions specified as `const`, all accessor (getters) should be `const` are not modifying the state of the objects in the class. The compiler prohibits them from chaning any of the objects's member data
  ```c
  #include <cassert>
  
  class Date {
  public:
    Date(int day, int month, int year);
    int Day() const { return day_; }
    void Day(int day);
    int Month() const { return month_; }
    void Month(int month);
    int Year() const { return year_; }
    void Year(int year);
  
  private:
    // const means these functions don't change the 
    // state of the objecst in this class
    bool LeapYear(int year) const;
    int DaysInMonth(int month, int year) const;
    int day_{1};
    int month_{1};
    int year_{0};
  };
  
  Date::Date(int day, int month, int year) {
    Year(year);
    Month(month);
    Day(day);
  }
  
  bool Date::LeapYear(int year) const {
      if(year % 4 != 0)
          return false;
      else if(year % 100 != 0)
          return true;
      else if(year % 400 != 0)
          return false;
      else
          return true;
  }
  
  int Date::DaysInMonth(int month, int year) const {
      if(month == 2)
          return LeapYear(year) ? 29 : 28;
      else if(month == 4 || month == 6 || month == 9 || month == 11)
          return 30;
      else
          return 31;
  }
  
  void Date::Day(int day) {
    // calling the accessors for Month and Year
    // instead of passing variables directly
    // more incapsulation
    if (day >= 1 && day <= DaysInMonth(Month(), Year()))
      day_ = day;
  }
  
  void Date::Month(int month) {
    if (month >= 1 && month <= 12)
      month_ = month;
  }
  
  void Date::Year(int year) { year_ = year; }
  
  // Test
  int main() {
    Date date(29, 2, 2016);
    assert(date.Day() == 29);
    assert(date.Month() == 2);
    assert(date.Year() == 2016);
      
    Date date2(29, 2, 2019);
    assert(date2.Day() != 29);
    assert(date2.Month() == 2);
    assert(date2.Year() == 2019);
  }
  ```
  
  ### Mutators
  - `mutators` or `setters` are public member functions that allow us to change the state of an object
  - we use mutator functions when there is some `invariant` to the class, like a logic or some limit to how we can the state of the class
  
  
  `abstractions` is the separaton of the class's interface from the details of its implementation.
  
  ### Static Member Functions
  - `static` member functions are instance-independent, they belong to the whole class, not to any particular instance
  - we can invoke a static member function *without ever creating an instance of the class*
  ```c
  #include <cassert>
  #include <cmath>
  
  class Sphere {
   public:
     static float Volume(int radius) {
         return pi_ * 4/3 * pow(radius,3);
     }
  
   private:
    static float constexpr pi_{3.14159};
  };
  
  // Test
  int main(void) {
    assert(abs(Sphere::Volume(5) - 523.6) < 1);
  }
  ```
  
  ## Inheritance
  [Standard C++](https://isocpp.org/wiki/faq/strange-inheritance)
  ```c
  // This example demonstrates the privacy levels
  // between parent and child classes
  #include <iostream>
  #include <string>
  using std::string;
  
  class Vehicle {
  public:
      int wheels = 0;
      string color = "blue";
      
      void Print() const
      {
          std::cout << "This " << color << " vehicle has " << wheels << " wheels!\\n";
      }
  };
  
  class Car : public Vehicle {
  public:
      bool sunroof = false;
  };
  
  class Bicycle : protected Vehicle {
  public:
      bool kickstand = true;
      void Wheels(int w)
      {
          wheels = w;
      }
  };
  
  class Scooter : private Vehicle {
  public:
      bool electric = false;
      void Wheels(int w)
      {
          wheels = w;
      }
  };
  
  
  class RaceBike : public Bicycle {
  
  };
  
  class PrivateRaceBike : private Bicycle {
  
  };
  
  int main() 
  {
      Car car;
      car.wheels = 4;
      Bicycle bicycle;
      // WILL NOT WORK
      // bicycle.wheels = 2;
      // in private inheritance you can only access parent class member through accessor functions
      bicycle.Wheels(2);
      Scooter scooter;
      // WILL NOT WORK
      // scooter.wheels = 2;
      scooter.Wheels(1);
      RaceBike racebike;
      racebike.Wheels(6); // works
      PrivateRaceBike privateracebike;
      // WILL NOT WORK Wheels() IS NOT ACESSIBLE
      // privateracebike.Wheels(6);
      // Wouldn't work with protected inheritance either
      
  };
  ```
  
  ### Friend Inheritance
  A `friend` class can have access to an other class's private variables.
  ```c++
  #include <cassert>
  
  class Heart {
  private:
      int rate{80};
      friend class Human;
  };
  
  class Human {
  public:
      Heart heart;
      void Exercise() { heart.rate = 150; }
      int HeartRate() { return heart.rate; }
  };
  
  int main() {
      Human human;
      assert(human.HeartRate() == 80);
      human.Exercise();
      assert(human.HeartRate() == 150);
  }
  ```
  ## Composition
  Composition involves constructing (composing) classes from other classes. If a class only needst o extend the functionality from an other class, we use `inheritance`, if it needs functionality from several different unrelated classes we use `composition`.
  `Inheritance`: **is a**, cat is a mammal
  `Composition`: **has a**, cat has a head, 4 paws...
  
  
  ## Multiple Inheritance:
  - use it to represent multiple distinct interfaces:
  [C++ Core Guidelines](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#c135-use-multiple-inheritance-to-represent-multiple-distinct-interfaces)
  - use it represent the union of implementation attributes:
  [C++ Core Guidelines](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#c136-use-multiple-inheritance-to-represent-the-union-of-implementation-attributes)
  
  ```c
  #include <cassert>
  #include <iostream>
  
  class Car {
  public:
      std::string Drive() { return "I'm driving"; }
  };
  
  class Boat {
  public:
      std::string Cruise() { return "I'm cruising"; }
  
  };
  
  // create class with multiple inheritance
  class AmphibiousCar : public Boat, public Car {};
  
  int main() {
      Car car;
      Boat boat;
      AmphibiousCar duck;
      assert(duck.Drive() == car.Drive());
      assert(duck.Cruise() == boat.Cruise());
  }
  ```
  ### Diamond problem
  
  - Take a Vehicle abstract class with a pure virtual function Move().
  - Take class Car and class Boat both inheriting from abstract class Vehicle, both defining Move() differently.
  - Take a class AmphibiousCar which inherits from both Car and Boat. If you call Move() on AmphibiousCar which Move() method is implemented?
  
  
  
'''
linesHighlighted: [
  5
]
isStarred: false
isTrashed: false
