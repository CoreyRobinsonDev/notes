
# Basic Types
- use `T(v)` to convert `v` to type `T`
- bool
- string
- int int8 int16 int32 int64
- uint uint8 uint16 uint32 uint64 uintptr
- byte *alias for uint8*
- rune *alias for int32*
- float32 float64
- complex64 complex128

# Zero Values
- variables declared without an explict intial value are given a *zero value*
- *zero values* are:
    - 0
    - false
    - ""

## Numberic Constants
- *numeric constants* are high-precision values

```go
    package main

    import "fmt"

    const (
        // Create a huge number by shifting a 1 bit left 100 places.
        // In other words, the binary number that is 1 followed by 100 zeroes.
        Big = 1 << 100
        // Shift it right again 99 places, so we end up with 1<<1, or 2.
        Small = Big >> 99
    )

    func needInt(x int) int { return x*10 + 1 }
    func needFloat(x float64) float64 {
        return x * 0.1
    }

    func main() {
        fmt.Println(needInt(Small))
        fmt.Println(needFloat(Small))
        fmt.Println(needFloat(Big))
    }
```
