# Strings
- strings are immutable
- use *+* to concatenate strings
- use the /*strings*/ package for useful functions

```go
    import "strings"

    strings.ToLower("MaKEmeLoweRCase") // => "makemelowercase"
    strings.Repeat("Go", 3) // => "GoGoGo"
```

# String Formatting
- use the *fmt* package for string formatting
- floating point values can be formatted with:
    - *%g* compact representation
    - *%e* exponent
    - *%f* non exponent

```go
    import "fmt"

    food := "taco"
    fmt.Sprintf("Bring me a %s", food) // => Bring me a taco
```

## String Functions
[source](https://gobyexample.com/string-functions)

```go
    package main

    import (
        "fmt"
        s "strings"
    )

    var p = fmt.Println

    func main() {

        p("Contains:  ", s.Contains("test", "es"))
        p("Count:     ", s.Count("test", "t"))
        p("HasPrefix: ", s.HasPrefix("test", "te"))
        p("HasSuffix: ", s.HasSuffix("test", "st"))
        p("Index:     ", s.Index("test", "e"))
        p("Join:      ", s.Join([]string{"a", "b"}, "-"))
        p("Repeat:    ", s.Repeat("a", 5))
        p("Replace:   ", s.Replace("foo", "o", "0", -1))
        p("Replace:   ", s.Replace("foo", "o", "0", 1))
        p("Split:     ", s.Split("a-b-c-d-e", "-"))
        p("ToLower:   ", s.ToLower("TEST"))
        p("ToUpper:   ", s.ToUpper("test"))
    }
```

## String Formatting
[source](https://gobyexample.com/string-formatting)

```go
    package main

    import (
        "fmt"
        "os"
    )

    type point struct {
        x, y int
    }

    func main() {

        p := point{1, 2}
        fmt.Printf("struct1: %v\n", p)

        fmt.Printf("struct2: %+v\n", p)

        fmt.Printf("struct3: %#v\n", p)

        fmt.Printf("type: %T\n", p)

        fmt.Printf("bool: %t\n", true)

        fmt.Printf("int: %d\n", 123)

        fmt.Printf("bin: %b\n", 14)

        fmt.Printf("char: %c\n", 33)

        fmt.Printf("hex: %x\n", 456)

        fmt.Printf("float1: %f\n", 78.9)

        fmt.Printf("float2: %e\n", 123400000.0)
        fmt.Printf("float3: %E\n", 123400000.0)

        fmt.Printf("str1: %s\n", "\"string\"")

        fmt.Printf("str2: %q\n", "\"string\"")

        fmt.Printf("str3: %x\n", "hex this")

        fmt.Printf("pointer: %p\n", &p)

        fmt.Printf("width1: |%6d|%6d|\n", 12, 345)

        fmt.Printf("width2: |%6.2f|%6.2f|\n", 1.2, 3.45)

        fmt.Printf("width3: |%-6.2f|%-6.2f|\n", 1.2, 3.45)

        fmt.Printf("width4: |%6s|%6s|\n", "foo", "b")

        fmt.Printf("width5: |%-6s|%-6s|\n", "foo", "b")

        s := fmt.Sprintf("sprintf: a %s", "string")
        fmt.Println(s)

        fmt.Fprintf(os.Stderr, "io: an %s\n", "error")
    }
    ```

    # Text Templates
    [source](https://gobyexample.com/text-templates)

    ```go
    package main

    import (
        "os"
        "text/template"
    )

    func main() {

        t1 := template.New("t1")
        t1, err := t1.Parse("Value is {{.}}\n")
        if err != nil {
            panic(err)
        }

        t1 = template.Must(t1.Parse("Value: {{.}}\n"))

        t1.Execute(os.Stdout, "some text")
        t1.Execute(os.Stdout, 5)
        t1.Execute(os.Stdout, []string{
            "Go",
            "Rust",
            "C++",
            "C#",
        })

        Create := func(name, t string) *template.Template {
            return template.Must(template.New(name).Parse(t))
        }

        t2 := Create("t2", "Name: {{.Name}}\n")

        t2.Execute(os.Stdout, struct {
            Name string
        }{"Jane Doe"})

        t2.Execute(os.Stdout, map[string]string{
            "Name": "Mickey Mouse",
        })

        t3 := Create("t3",
            "{{if . -}} yes {{else -}} no {{end}}\n")
        t3.Execute(os.Stdout, "not empty")
        t3.Execute(os.Stdout, "")

        t4 := Create("t4",
            "Range: {{range .}}{{.}} {{end}}\n")
        t4.Execute(os.Stdout,
            []string{
                "Go",
                "Rust",
                "C++",
                "C#",
            })
    }
    ```

    # Regular Expressions
    [source](https://gobyexample.com/regular-expressions)

    ```go
    package main

    import (
        "bytes"
        "fmt"
        "regexp"
    )

    func main() {

        match, _ := regexp.MatchString("p([a-z]+)ch", "peach")
        fmt.Println(match)

        r, _ := regexp.Compile("p([a-z]+)ch")

        fmt.Println(r.MatchString("peach"))

        fmt.Println(r.FindString("peach punch"))

        fmt.Println("idx:", r.FindStringIndex("peach punch"))

        fmt.Println(r.FindStringSubmatch("peach punch"))

        fmt.Println(r.FindStringSubmatchIndex("peach punch"))

        fmt.Println(r.FindAllString("peach punch pinch", -1))

        fmt.Println("all:", r.FindAllStringSubmatchIndex(
            "peach punch pinch", -1))

        fmt.Println(r.FindAllString("peach punch pinch", 2))

        fmt.Println(r.Match([]byte("peach")))

        r = regexp.MustCompile("p([a-z]+)ch")
        fmt.Println("regexp:", r)

        fmt.Println(r.ReplaceAllString("a peach", "<fruit>"))

        in := []byte("a peach")
        out := r.ReplaceAllFunc(in, bytes.ToUpper)
        fmt.Println(string(out))
    }
```
