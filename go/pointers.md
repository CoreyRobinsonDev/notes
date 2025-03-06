# Pointers
- *pointers* hold a memory address
- a zero value pointer is *nil*
- use **&** to get the memory address of a variable
- use * to dereference a pointer

```go
var p *int // 'p' is initially nil

var a int
a = 2

p = &a // 'p' contains the memory address of 'a'
b = *p // 'b' contains the value of 'a'
```

## Pointers to Structs
```go
import "fmt"

type Person struct {
    Name string
    Age int
}

var p *Person
p = &Person { Name: "Peter", Age: 22 }

fmt.Println(p.Name) // => "Peter"
// 'p' is automatically dereferenced
```
