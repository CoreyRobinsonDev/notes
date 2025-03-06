
# Exiting
[source](https://gobyexample.com/exit)

```go
    package main

    import (
        "fmt"
        "os"
    )

    func main() {
        defer fmt.Println("!")
        os.Exit(3)
    }
```

