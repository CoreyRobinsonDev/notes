# Struct
- fields that do not have an initial value will have a *zero value*
- *struct* instance can be created without field names as long as fields are defined in order

```go
    type Shape struct {
        name string
        size int
    }

    s := Shape {
        name: "Square",
        size: 25,
    }

    s.name = "Circle"
    s.size = 30

    s := Shape { "Circle", 20 }
```

# Methods
- a *method* is just a *function* with a *receiver* argument
- there are 2 types of receivers
    - value receivers (copies the value)
    - pointer receivers (modifies the value through reference)


```go
package person

import "fmt"

type Person struct {
    Name string
}

func (self Person) Greetings() string {
    return fmt.Sprintf("Welcome %s!", self.Name)
}

func (self *Person) Rename(name string) {
    self.Name = name
}

p := Person { Name: "Bob" }
fmt.Println(p.Greetings()) // => "Welcome Bob!"
```

# Struct Embedding
```go
import "fmt"

type base struct {
    num int
}

func (b base) describe() string {
    return fmt.Sprintf("base with num=%v", b.num)
}

type container struct {
    base
    str string
}

func main() {
    co := container {
        base: base {
            num: 1,
        },
        str: "name"
    }

    // both ways of accessing are valid
    fmt.Printf("co={num: %v, str: %v}\n", co.num, co.str)
    fmt.Printf("co={num: %v, str: %v}\n", co.base.num, co.str)

    fmt.Printf("describe: ", co.describe())
}

```
