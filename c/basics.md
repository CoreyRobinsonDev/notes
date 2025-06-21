# Compiling
```bash
gcc -o <program-name> <program-name>.c
```
# Types
|type|size (bits)|min|max|
|-|--|--|--|
|char|8|-128|127|
|unsigned char|8|0|255|
|short|16|-32,768|32,767|
|unsigned short|16|0|65,535|
|int|16 or 32|-2,147,483,648|2,147,483,647|
|unsigned int|16 or 32|0|4,294,967,295|
|long|32|-2,147,483,648|2,147,483,647|
|unsigned long|32|0|4,294,967,295|
|long long|64|-9,223,372,036,854,775,808|9,223,372,036,854,775,807|
|unsigned long long|64|0|18,446,744,073,709,551,615|
|float|32|~ -3.4 x 10^38|~ 3.4 x 10^38|
|double|64|~ -1.7 x 10^308|~ 1.7 x 10^308|

## Modifiers
- use `const` to declare a read-only variable
- use `static` within a function scope to persist the value across multiple function calls
- use `static` within a global scope to make the variable visible only within the current source file

## Type Casting
```c
int other_var = -1;
unsigned int x = (unsigned int)other_var;
```
### Up Casting
```c
short other_var = -1;
int x = (int)other_var;
```
### Down Casting
- the value will be trunctated to fit the new size
```c
int other_var = -1;
short x = (short)other_var;
```

# Arrays
```c
int ids[10];
int ids2[] = {1,2,3,4,5,6,7,8,9,10};
```
# Strings
- **strings** are zero-delimited
```c
char my_str[] = {'h','e','l','l','o',0};
char* my_str2 = "hello";
```
