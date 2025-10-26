---
tags:
  - cpp
  - programming
source: https://www.learncpp.com/cpp-tutorial/a1-static-and-dynamic-libraries/
---
## Static(Archive) and Dynamic(Shared) Libraries

Compiling code with a static library includes all the functionality of the static library, that is used, into my executable. Usually compiled into .a file format, the executable contains the exact version of the library that is used and allow you to use the included code as you would use your code. Every executable contains the copy of the static library and upgrading them can be more complicated

Compiling code with the dynamic library does combine the compiled units, instead they are separate. Typically .so format, these libraries can be shared between different executables, and upgraded at their own rate without having to replace all of the consumers of the library. These libraries must be loaded at run time to be interfaced with, which can conflicts in the usage, that is mitigated by using an import library that automates the library loading, and simplifies the process.  

> [!question]
> is there any significant computational effeciency between static and dynamic libraries?


