# Detecting Memory Leaks
## Valgrind
- to use **Valgrind** you must do the following
    1. Compile with debug symbols using the `-g` flag
    ```bash
    gcc -o <programe-name> <program-name>.c -g
    ```
    2. Run **Valgrind**
    ```bash
    valgrind --leak-check=full ./<program-name> -s
    ```
