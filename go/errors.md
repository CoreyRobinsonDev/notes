# Errors
[source](https://gobyexample.com/errors)

```go
    package main

    import (
        "errors"
        "fmt"
    )

    func f(arg int) (int, error) {
        if arg == 42 {

            return -1, errors.New("can't work with 42")
        }

        return arg + 3, nil
    }

    var ErrOutOfTea = fmt.Errorf("no more tea available")
    var ErrPower = fmt.Errorf("can't boil water")

    func makeTea(arg int) error {
        if arg == 2 {
            return ErrOutOfTea
        } else if arg == 4 {

            return fmt.Errorf("making tea: %w", ErrPower)
        }
        return nil
    }

    func main() {
        for _, i := range []int{7, 42} {

            if r, e := f(i); e != nil {
                fmt.Println("f failed:", e)
            } else {
                fmt.Println("f worked:", r)
            }
        }

        for i := range 5 {
            if err := makeTea(i); err != nil {

                if errors.Is(err, ErrOutOfTea) {
                    fmt.Println("We should buy new tea!")
                } else if errors.Is(err, ErrPower) {
                    fmt.Println("Now it is dark.")
                } else {
                    fmt.Printf("unknown error: %s\n", err)
                }
                continue
            }

            fmt.Println("Tea is ready!")
        }
    }
```

# Custom Errors
[source](https://gobyexample.com/custom-errors)
- custom errors must implement the error interface

```go
    package main

    import (
        "errors"
        "fmt"
    )

    type argError struct {
        arg     int
        message string
    }

    func (e *argError) Error() string {
        return fmt.Sprintf("%d - %s", e.arg, e.message)
    }

    func f(arg int) (int, error) {
        if arg == 42 {

            return -1, &argError{arg, "can't work with it"}
        }
        return arg + 3, nil
    }

    func main() {

        _, err := f(42)
        var ae *argError
        if errors.As(err, &ae) {
            fmt.Println(ae.arg)
            fmt.Println(ae.message)
        } else {
            fmt.Println("err doesn't match argError")
        }
    }
```
