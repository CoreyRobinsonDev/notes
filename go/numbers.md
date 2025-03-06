# Numbers
## Int
- a signed integer of at least 32bits
- most likely 64bit in size on modern systems

## Float
- *float32* has ~6-9 digit percision
- *float64* has ~15-17 digit percision
- *float64* is the default float type

```go
var x int = 42 // x has type int
f := float64(x) // f has type float64 (ie. 42.0)
var y float64 = 11.9 // y has type float64
i := int(y) // i has type int (ie. 11)
```

# Operators
## Arithmetic
- Operations cannot be performed between different types
- **(+ += ++ - -= -- * / %)**

## Bitwise
- **(& | ^ << >>)**

# Random Numbers
[source](https://gobyexample.com/random-numbers)

```go
package main

import (
    "fmt"
    "math/rand/v2"
)

func main() {

    fmt.Print(rand.IntN(100), ",")
    fmt.Print(rand.IntN(100))
    fmt.Println()

    fmt.Println(rand.Float64())

    fmt.Print((rand.Float64()*5)+5, ",")
    fmt.Print((rand.Float64() * 5) + 5)
    fmt.Println()

    s2 := rand.NewPCG(42, 1024)
    r2 := rand.New(s2)
    fmt.Print(r2.IntN(100), ",")
    fmt.Print(r2.IntN(100))
    fmt.Println()

    s3 := rand.NewPCG(42, 1024)
    r3 := rand.New(s3)
    fmt.Print(r3.IntN(100), ",")
    fmt.Print(r3.IntN(100))
    fmt.Println()
}
```

## Number Parsing
[source](https://gobyexample.com/number-parsing)

```go
package main

import (
    "fmt"
    "strconv"
)

func main() {

    f, _ := strconv.ParseFloat("1.234", 64)
    fmt.Println(f)

    i, _ := strconv.ParseInt("123", 0, 64)
    fmt.Println(i)

    d, _ := strconv.ParseInt("0x1c8", 0, 64)
    fmt.Println(d)

    u, _ := strconv.ParseUint("789", 0, 64)
    fmt.Println(u)

    k, _ := strconv.Atoi("135")
    fmt.Println(k)

    _, e := strconv.Atoi("wat")
    fmt.Println(e)
}
```
