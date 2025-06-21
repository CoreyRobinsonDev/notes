# Make
```make
TARGET = bin/final
SRC = $(wildcard src/*.c)
OBJ = $(patsubst src/%.c, obj/%.o, $(SRC))

run: clean default
    @./$(TARGET)

default: $(TARGET)

clean: 
    @rm -f obj/*.o
    @rm -f bin/*

$(TARGET): $(OBJ)
    @gcc -o $@ $?

obj/%.o : src/%.c
    @gcc -c $< -o $@ -Iinclude
```

# Creating Libraries
- library files must begin with *lib*
## Shared Object
- **shared objects** get loaded outside of the progrem ELF (executable and linkable file) and the loader will build a link between the two at *runtime*
- to create a **shared object** do the following:
    1. Create the **shared object**
    `gcc -o <lib-name>.so <lib-name>.c -shared`
    1. Move the archive file to the main program dirctory
    1. Compile the main program
    `gcc -o <prog-name> <prog-name.c -I<header-directory> -l<lib-name-without-'lib'> -L<lib-search-path>`
    1. Running the program
        - with library within local path
        `LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$(pwd) ./<prog-name>`
        - with library installed on system
        ```bash
        sudo mv <lib-name>.so /usr/lib
        ./<prog-name>
        ```

## Static Object
- **static objects** are compressed and loaded in at *compiletime*
- to create a **static object** do the following:
    1. Create an intermediate object
    `gcc -o <lib-name>.o -c <lib-name>.c`
    1. Create an archive file
    `ar rcs <lib-name>.a <lib-name>.o`
    1. Move the archive file to the main program dirctory
    1. Compile the main program
    `gcc -o <prog-name> <prog-name.c <lib-name>.a -I<header-directory>`

