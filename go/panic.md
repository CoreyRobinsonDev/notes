# Panic
[source](https://gobyexample.com/panic)

```go
package main

import "os"

func main() {

    panic("a problem")

    _, err := os.Create("/tmp/file")
    if err != nil {
        panic(err)
    }
}
```

# Recover
[source](https://gobyexample.com/recover)

- use `recover()` to come back from a panic
- `recover()` must be called within a *deferred* funciton

```go
package main

import "fmt"

func mayPanic() {
    panic("a problem")
}

func main() {

    defer func() {
        if r := recover(); r != nil {

            fmt.Println("Recovered. Error:\n", r)
        }
    }()

    mayPanic()

    fmt.Println("After mayPanic()")
}
```
