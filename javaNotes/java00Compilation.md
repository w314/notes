java, compilation, jdk, jre, jvm, jit

# Java Compilation Process

Sources:
- [jvm-vs-jre-vs-jdk](https://www.ibm.com/blog/jvm-vs-jre-vs-jdk/
)

## Compilation

Compilation transforms a program written in a high-level programming language from `source code` into `object code` / `bytecode`

Compilation Types:
- **static** - converts source code into a form that can be run on a platform
- **interpreter** - directly executes the code
- **dynamic** (**JIT**) - combines the two above <br>
    - while the interpreter runs the JIT complier determines the most frequently used code and turns it into machine code
    - JIT or dynamic compilation is compilation that being done during program execution


## Java Compilation Process

The 2 steps compilation process:

1. compiler creates machine independent `bytecode` (`.java` -> `.class`)
```bash
#  command to compile .java file
javac myFile.java
```
2. `JVM` creates machine code
```bash
# command to run java program (.class file)
java myFile
```

## JIT (Just In Time) Compiler
> Turns Java bytecode to machine code
- Combines static compilation with interpreting the code
- while the interpreter runs 

## JVM vs JRE vs JDK

### JVM (Java Virtual Machine)
> Converts bytecode to machine code

- runs compiled bytecode (that is the same accress every platform) in a virtual environment 
- platform specific You need JVM that is specific to the operating system of the machine it runs on
- does memory management and security
- uses `JIT` `Just In Time` compiler to turn bytecode to machine code.

### JRE (Java Runtime Environment)
> Executes Java programs. Includes JVM and runtime libraries.

`JRE`  contains `JVM` and runtime libraries.

Examples:
 - Java Database Connectivity (JDBC) API
 - utility libraries like : Java.lang, Java.util

### JDK (Java Development Kit)
> The devlopment kit that includes JRE, a Java compiler, a debugger and other tools.

`JDK` `Java Development Kit` contains `JRE` and development tools like compiler, debugger, documentation tools.


## Java Compilation Questions
- What is the difference between source code and bytecode?
- How would you describe the compilation process for Java?
- What is the difference between the JDK, JRE, and JVM?
- What does System.exit(0) do?
