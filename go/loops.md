# For Loop
```go
for i := 0; i < 10; i++ {
    fmt.Println(i)
}
```
## Range Iteration
- *range* allows you to iterate of a *slice* or *map*
- iteration over a map is done in random order

```go
import "fmt"

xi := []int{10,20,30}

for i, x := range xi {
    fmt.Println(i,x)
}
// => 0 10
// => 1 20
// => 2 30

hash := map[int]int{
    9: 10,
    99: 20,
    999: 30
}

for k, v := range hash {
    fmt.Println(k, v)
}
// => 99 20
// => 999 30
// => 9 10
```


