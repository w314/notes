createdAt: "2021-01-18T16:37:41.369Z"
updatedAt: "2021-03-02T19:07:00.229Z"
type: "MARKDOWN_NOTE"
folder: "bb83f5f87373282090b3"
title: "C++ Loops"
tags: [
  "c"
  "for"
  "print"
  "cout"
  "iterator"
]
content: '''
  # C++ Loops
  
  ## For Loop
  
  ```c
  #include <iostream>
  using std::cout;
  
  int main() {
    for (int i=0; i<5; i++) {
      cout << i << "\\n";
    }
  }
  ```
  
  ### range based loops
  
  ```c
  #include <iostream>
  #include <vector>
  using std::cout;
  using std::vector;
  
  int main() {
    vector<int> a{1, 2, 3};
    for (int i: a) {
      cout << i << "\\n";
    }
  }
  ```
  
  ### double for loop
  ```c
  #include <iostream>
  #include <vector>
  using std::cout;
  using std::vector;
  
  vector<vector<int>> b {{1, 2}
                        {3, 4}
                        {5, 6}};
  
  // auto lets compiler decide variale type
  // could have used vector too
  for(auto v: b) {
    for(int i: v) {
      cout << i << "\\n";
    }
    cout << "\\n";
  }
  ```
  
  ### using an iterator
  ```c
  #include <iostream>
  #include <vector>
  using std::cout;
  using std::vector;
  
  int main() {
    vector<int> v{1, 2, 3};
    
    int sum = 0;
    // using auto for i as i now is an interator
    // not an int
    for(auto i = v.begin(); i != v.end(); i++) {
      // * wil get the value of the iterator
      sum += *i;
    }
    
    cout << sum << "/n";
  }
  ```
'''
linesHighlighted: []
isStarred: false
isTrashed: false
