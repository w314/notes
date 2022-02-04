createdAt: "2021-01-26T15:43:21.306Z"
updatedAt: "2021-07-12T20:30:08.814Z"
type: "MARKDOWN_NOTE"
folder: "bb83f5f87373282090b3"
title: "C++ Basics"
tags: [
  "c++"
  "compile"
  "g++"
]
content: '''
  # C++ Basics
  ## Style
  There are many different C++ styles, none of which is authoritative.
  - [C++ Core Guidelines](http://isocpp.github.io/CppCoreGuidelines/CppCoreGuidelines#nl-naming-and-layout-rules)
  
  `clang-format` is a command line text formatter that automatically reformats source code according to configurable set of policies. The tool includes several pre-configured styles, or you can create your own.
  
  clang-format is an open-source application that you can install on your system, or it is straightforward to install as a Visual Studio Code extension.
  
  ## Compilation process
  ### Object Files
  
  When you compile a project with g++, g++ actually performs several distinct tasks:
  
  - The preprocessor runs and **executes any statement beginning with a hash symbol: #**, such as #include statements. This ensures all code is in the correct location and ready to compile.
  - Each file in the source **code is compiled into an "object file" (a .o file). Object files are platform-specific machine code** that will be used to create an executable.
  - The **object files are "linked" together to make a single executable**. In the examples you have seen so far, this executable is a.out, but you can specify whatever name you want.
  
  It is possible to have g++ perform each of the steps separately by using the -c flag. To create the objcet file run:
  `g++ -c main.cpp`
  
  It will produce a main.o file, and that file can be converted to an executable with:
  `g++ main.o`
  
  ### Working with mulitple files
  
  Use `*` to run command on all files in a directory.
  - `g++ -c *.cpp` to create object files
  - `g++ *.o` to create executable 
  - `./a.out` to run executable
  
  Compilation can take a long time, if only one file has changed you can recreate its object file and use the formerly created object files of the other files:
  `g++ -c main.cpp`  > `g++ *.o` > `./a.out`
  
  ## Build Systems
  
  Build systems tracks what files have changed and complies only the necessary ones.
  
  ### CMake
  - open source, platform independent build system
  - uses text documents `CMakeLists.txt` files to manage build environtments. Each project directory can have its own CMakeList.txt file.
  
  
  #### CMakeList.txt Example
  
  ```c
  // first define minimum version of cmake and c++
  // required to build the project
  cmake_minimum_required(VERSION 3.5.1)
  set(CMAKE_CXX_STANDARD 14)
  
  // name the project
  project(<your_project_name)
  
  // add executable to the project
  add_exetuble(<your_exetuble_name> <path_to_file1> 
  <path_to_file_n>)
  ```
  
  ##### Run CMake/Make
  - Typical CMake project will have a `build` directory in the same place as the top level CMakeList.txt.
  - You run CMake from this build directory with commands:
  `cmake ..` first and then `make`
  - `cmake ..` directs the cmake command at the top level CMakeList.txt file with `..`. It uses the CMakeList.txt file to configure the project and create a `Makefile` in the build directory.
  - `make` will uses the instructions in the `Makefile` to build the project
  
  Unless build options change cmake only needs to be run once. Make keeps track of file changes and compile only those before build. So you'll only need to run make.
'''
linesHighlighted: []
isStarred: false
isTrashed: false
