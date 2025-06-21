# Preprocessors
- use `#include` to include a header file
- use `#define` to define a macro or constant
```c
#define PI 3.14
#define MAX(a,b) ((a) > (b) ? (a) ? (b))
```
- use `#undef` to undefine a macro
- use `#if`, `#elif` and `#else` to check if a condition is true
```c
#if DEBUG_MODE
printf("Debug mode enabled\n")
#endif
```
- use `#ifndef` to check if a macro is not defined
```c
#ifndef MY_HEADER_H
#define MY_HEADER_H
    // Header content
#endif
```
- use `#error` to emit an error message and stop compilation
- use `#warning` to emit an warning message and continue compilation
- use `#pragma` to provide compiler specific directives
- use `#line` to change the current line number and optionally file name reported to the compiler
