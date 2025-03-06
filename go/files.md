# Reading Files
[source](https://gobyexample.com/reading-files)


```go
    package main

    import (
        "bufio"
        "fmt"
        "io"
        "os"
    )

    func check(e error) {
        if e != nil {
            panic(e)
        }
    }

    func main() {
        dat, err := os.ReadFile("/tmp/dat")
        check(err)
        fmt.Print(string(dat))

        f, err := os.Open("/tmp/dat")
        check(err)

        b1 := make([]byte, 5)
        n1, err := f.Read(b1)
        check(err)
        fmt.Printf("%d bytes: %s\n", n1, string(b1[:n1]))

        o2, err := f.Seek(6, io.SeekStart)
        check(err)
        b2 := make([]byte, 2)
        n2, err := f.Read(b2)
        check(err)
        fmt.Printf("%d bytes @ %d: ", n2, o2)
        fmt.Printf("%v\n", string(b2[:n2]))

        _, err = f.Seek(4, io.SeekCurrent)
        check(err)

        _, err = f.Seek(-10, io.SeekEnd)
        check(err)

        o3, err := f.Seek(6, io.SeekStart)
        check(err)
        b3 := make([]byte, 2)
        n3, err := io.ReadAtLeast(f, b3, 2)
        check(err)
        fmt.Printf("%d bytes @ %d: %s\n", n3, o3, string(b3))

        _, err = f.Seek(0, io.SeekStart)
        check(err)

        r4 := bufio.NewReader(f)
        b4, err := r4.Peek(5)
        check(err)
        fmt.Printf("5 bytes: %s\n", string(b4))

        f.Close()
    }
```

# Writing Files
[source](https://gobyexample.com/writing-files)

```go
    package main

    import (
        "bufio"
        "fmt"
        "os"
    )

    func check(e error) {
        if e != nil {
            panic(e)
        }
    }

    func main() {

        d1 := []byte("hello\ngo\n")
        err := os.WriteFile("/tmp/dat1", d1, 0644)
        check(err)

        f, err := os.Create("/tmp/dat2")
        check(err)

        defer f.Close()

        d2 := []byte{115, 111, 109, 101, 10}
        n2, err := f.Write(d2)
        check(err)
        fmt.Printf("wrote %d bytes\n", n2)

        n3, err := f.WriteString("writes\n")
        check(err)
        fmt.Printf("wrote %d bytes\n", n3)

        f.Sync()

        w := bufio.NewWriter(f)
        n4, err := w.WriteString("buffered\n")
        check(err)
        fmt.Printf("wrote %d bytes\n", n4)

        w.Flush()

    }
```

## Line Filter
[source](https://gobyexample.com/line-filters)

- a common type of program that reads input on stdin, process it, and prints to stdout

```go
    package main

    import (
        "bufio"
        "fmt"
        "os"
        "strings"
    )

    func main() {

        scanner := bufio.NewScanner(os.Stdin)

        for scanner.Scan() {

            ucl := strings.ToUpper(scanner.Text())

            fmt.Println(ucl)
        }

        if err := scanner.Err(); err != nil {
            fmt.Fprintln(os.Stderr, "error:", err)
            os.Exit(1)
        }
    }
```

## File Paths
[source](https://gobyexample.com/file-paths)

- *filepath* package provides functions to parse and construct file paths

```go
    package main

    import (
        "fmt"
        "path/filepath"
        "strings"
    )

    func main() {
        p := filepath.Join("dir1", "dir2", "filename")
        fmt.Println("p:", p)

        fmt.Println(filepath.Join("dir1//", "filename"))
        fmt.Println(filepath.Join("dir1/../dir1", "filename"))

        fmt.Println("Dir(p):", filepath.Dir(p))
        fmt.Println("Base(p):", filepath.Base(p))

        fmt.Println(filepath.IsAbs("dir/file"))
        fmt.Println(filepath.IsAbs("/dir/file"))

        filename := "config.json"

        ext := filepath.Ext(filename)
        fmt.Println(ext)

        fmt.Println(strings.TrimSuffix(filename, ext))

        rel, err := filepath.Rel("a/b", "a/b/t/file")
        if err != nil {
            panic(err)
        }
        fmt.Println(rel)

        rel, err = filepath.Rel("a/b", "a/c/t/file")
        if err != nil {
            panic(err)
        }
        fmt.Println(rel)
    }
```

### Directories
[source](https://gobyexample.com/directories)

```go
    package main

    import (
        "fmt"
        "io/fs"
        "os"
        "path/filepath"
    )

    func check(e error) {
        if e != nil {
            panic(e)
        }
    }

    func main() {

        err := os.Mkdir("subdir", 0755)
        check(err)

        defer os.RemoveAll("subdir")

        createEmptyFile := func(name string) {
            d := []byte("")
            check(os.WriteFile(name, d, 0644))
        }

        createEmptyFile("subdir/file1")

        err = os.MkdirAll("subdir/parent/child", 0755)
        check(err)

        createEmptyFile("subdir/parent/file2")
        createEmptyFile("subdir/parent/file3")
        createEmptyFile("subdir/parent/child/file4")

        c, err := os.ReadDir("subdir/parent")
        check(err)

        fmt.Println("Listing subdir/parent")
        for _, entry := range c {
            fmt.Println(" ", entry.Name(), entry.IsDir())
        }

        err = os.Chdir("subdir/parent/child")
        check(err)

        c, err = os.ReadDir(".")
        check(err)

        fmt.Println("Listing subdir/parent/child")
        for _, entry := range c {
            fmt.Println(" ", entry.Name(), entry.IsDir())
        }

        err = os.Chdir("../../..")
        check(err)

        fmt.Println("Visiting subdir")
        err = filepath.WalkDir("subdir", visit)
    }

    func visit(path string, d fs.DirEntry, err error) error {
        if err != nil {
            return err
        }
        fmt.Println(" ", path, d.IsDir())
        return nil
    }
```

### Temp Files and Directories
[source](https://gobyexample.com/temporary-files-and-directories)

```go
    package main

    import (
        "fmt"
        "os"
        "path/filepath"
    )

    func check(e error) {
        if e != nil {
            panic(e)
        }
    }

    func main() {

        f, err := os.CreateTemp("", "sample")
        check(err)

        fmt.Println("Temp file name:", f.Name())

        defer os.Remove(f.Name())

        _, err = f.Write([]byte{1, 2, 3, 4})
        check(err)

        dname, err := os.MkdirTemp("", "sampledir")
        check(err)
        fmt.Println("Temp dir name:", dname)

        defer os.RemoveAll(dname)

        fname := filepath.Join(dname, "file1")
        err = os.WriteFile(fname, []byte{1, 2}, 0666)
        check(err)
    }
```

## Embed Directive
[source](https://gobyexample.com/embed-directive)

- `//go:embed` is a compiler directive that allows programs to include arbitrary files and folders in the go binary at build time

```go
    package main

    import (
        "embed"
    )

    //go:embed folder/single_file.txt
    var fileString string

    //go:embed folder/single_file.txt
    var fileByte []byte

    //go:embed folder/single_file.txt
    //go:embed folder/*.hash
    var folder embed.FS

    func main() {

        print(fileString)
        print(string(fileByte))

        content1, _ := folder.ReadFile("folder/file1.hash")
        print(string(content1))

        content2, _ := folder.ReadFile("folder/file2.hash")
        print(string(content2))
    }
```
