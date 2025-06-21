# Error Checking
- **errno** is a global number within libc
- use `perror(<function-name>)` to print the error message associated with that function
```c
#include <stdio.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>

int main() {
    int fd = open("./asdf", O_RDONLY);
    if (fd == -1) {
        perror("open");
        return -1;
    }
}
```
