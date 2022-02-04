createdAt: "2021-02-23T16:13:20.998Z"
updatedAt: "2021-02-23T18:22:58.811Z"
type: "MARKDOWN_NOTE"
folder: "bb83f5f87373282090b3"
title: "C++ File Management"
tags: []
content: '''
  # C++ File Management
  ## Read from file
  
  The `std::ifstream` object can handle input file streams.
  
  ```c
  #include <fstream>
  #include <string>
  #inlcude <iostream>
  
  int main() {
    // new input stream object is declared
    std::ifstream my_file;
    // and initialized with a path
    std::string path = "files/1.board";
    my_file.open(path);
    
    /*
    OR
    
  
  
    //reading from file
    if (my_file) {
      std::string line;
      while (getline(my_file, line)) {
        std::cout << line << "\\n";
      }
    }
  }
  ```
  
  ### Read interger from file
  
  Streaming a string allows us to work with each character individually.
  One way to stream a string is using the `istringstream` string stream object from the `<sstream>` header.
  Once the `istrinstream` object was created parts of the string can be stream with the `extraction operator` `>>`. The extraction operator will read until whitespace is reached or until the stream fails.
  ```c
  #include <iostream>
  #include <sstream>
  #include <string>
  
  using std::istringstream;
  using std::string;
  using std::cout;
  
  int main () {
      string a("1 2 3");
  
      istringstream my_stream(a);
      
      int n;
      
      while (my_stream >> n) {
        cout << "That stream was successful: " << n << "\\n";
      }
      cout << "The stream has failed." << "\\n";
      
  }
  ```
'''
linesHighlighted: []
isStarred: false
isTrashed: false
