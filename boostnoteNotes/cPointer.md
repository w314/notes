createdAt: "2021-03-02T19:07:16.351Z"
updatedAt: "2021-03-04T14:13:56.327Z"
type: "MARKDOWN_NOTE"
folder: "bb83f5f87373282090b3"
title: "C++ Pointers"
tags: []
content: '''
  # C++ Pointers
  
  ## Accessing a Memory Address
  Each variable in a program stores its contents in the computer's memory, and each chunk of the memory has an address number. For a given variable, the memory address can be accessed using an ampersand in front of the variable. To see an example of this, execute the following code which displays the hexadecimal memory addresses of the variables i and j:
  ```c++
  #include <iostream>
  using std::cout;
  
  int main() {
      int i = 5;
      int j = 6;
      
      // Print the memory addresses of i and j
      cout << "The address of i is: " << &i << "\\n";
      cout << "The address of j is: " << &j << "\\n";
  }
  ```
  
  At this point, you might be wondering why the same symbol & can be used to both access memory addresses and, as you've seen before, pass references into a function. This is a great thing to wonder about. The overloading of the ampersand symbol & and the * symbol probably contribute to much of the confusion around pointers.
  
  **The symbols `&` and `*` have a different meaning, depending on which side of an equation they appear.**
  
  This is extremely important to remember. For the & symbol, if it appears on the left side of an equation (e.g. when declaring a variable), it means that the variable is declared as a reference. If the & appears on the right side of an equation, or before a previously defined variable, it is used to return a memory address, as in the example above.
  
  ## Storing a Memory Address (int type)
  Once a memory address is accessed, you can store it using a pointer. A pointer can be declared by using the * operator in the declaration. See the following code for an example:
  ```c++
  #include <iostream>
  using std::cout;
  
  int main() 
  {
      int i = 5;
      // A pointer pointer_to_i is declared and initialized to the address of i.
      int* pointer_to_i = &i;
      
      // Print the memory addresses of i and j
      cout << "The address of i is:          " << &i << "\\n";
      cout << "The variable pointer_to_i is: " << pointer_to_i << "\\n";
  }
  ```
  
  As you can see from the code, the variable pointer_to_i is declared as a pointer to an int using the * symbol, and pointer_to_i is set to the address of i. From the printout, it can be seen that pointer_to_i holds the same value as the address of i.
  
  ## Getting an Object Back from a Pointer Address
  Once you have a pointer, you may want to retrieve the object it is pointing to. In this case, the * symbol can be used again. This time, however, it will appear on the right hand side of an equation or in front of an already-defined variable, so the meaning is different. In this case, it is called the "dereferencing operator", and it returns the object being pointed to. You can see how this works with the code below:
  ```c++
  #include <iostream>
  using std::cout;
  
  int main() 
  {
      int i = 5;
      // A pointer pointer_to_i is declared and initialized to the address of i.
      int* pointer_to_i = &i;
      
      // Print the memory addresses of i and j
      cout << "The address of i is:          " << &i << "\\n";
      cout << "The variable pointer_to_i is: " << pointer_to_i << "\\n";
      cout << "The value of the variable pointed to by pointer_to_i is: " << *pointer_to_i << "\\n";
  }
  ```
  
  In the following example, the code is similar to above, except that the object that is being pointed to is changed before the pointer is dereferenced. Before executing the following code, guess what you think will happen to the value of the dereferenced pointer.
  
  ```c++
  #include <iostream>
  using std::cout;
  
  int main() {
      int i = 5;
      // A pointer pointer_to_i is declared and initialized to the address of i.
      int* pointer_to_i = &i;
      
      // Print the memory addresses of i and j
      cout << "The address of i is:          " << &i << "\\n";
      cout << "The variable pointer_to_i is: " << pointer_to_i << "\\n";
      
      // The value of i is changed.
      i = 7;
      cout << "The new value of the variable i is                     : " << i << "\\n";
      cout << "The value of the variable pointed to by pointer_to_i is: " << *pointer_to_i << "\\n";
      cout << "The variable pointer_to_i is: " << pointer_to_i << "\\n";
  }
  ```
  As you can see, an object or variable can be changed while a pointer is pointing to it.
  
  ## References vs Pointers
  
  A reference can only point to one thing. If i want you to work with my object i can give you a reference to it and you can work with that object, but cannot point the reference to any other object of mine. If i give you a pointer, you can change that to an other address.
  
  Pointers and references can have similar use cases in C++. As seen previously both references and pointers can be used in pass-by-reference to a function. Additionally, they both provide an alternative way to access an existing variable: pointers through the variable's address, and references through another name for that variable. But what are the differences between the two, and when should each be used? The following list summarizes some of the differences between pointers and references, as well as when each should be used:
  
  References	Pointers
  References must be initialized when they are declared. This means that a reference will always point to data that was intentionally assigned to it.	Pointers can be declared without being initialized, which is dangerous. If this happens mistakenly, the pointer could be pointing to an arbitrary address in memory, and the data associated with that address could be meaningless, leading to undefined behavior and difficult-to-resolve bugs.
  References can not be null. This means that a reference should point to meaningful data in the program.	Pointers can be null. In fact, if a pointer is not initialized immediately, it is often best practice to initialize to nullptr, a special type which indicates that the pointer is null.
  When used in a function for pass-by-reference, the reference can be used just as a variable of the same type would be.	When used in a function for pass-by-reference, a pointer must be dereferenced in order to access the underlying object.
  References are generally easier and safer than pointers. As a decent rule of thumb, references should be used in place of pointers when possible.
  
  However, there are times when it is not possible to use references. One example is object initialization. You might like one object to store a reference to another object. However, if the other object is not yet available when the first object is created, then the first object will need to use a pointer, not a reference, since a reference cannot be null. The reference could only be initialized once the other object is created.
  
'''
linesHighlighted: [
  44
  87
]
isStarred: false
isTrashed: false
