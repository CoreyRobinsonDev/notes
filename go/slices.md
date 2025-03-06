# Slices
- /slices/ are based on arrays
- /slices/ are dynamically sized
- a range of elements can be selected by setting the *start (inclusive):end (exclusive)*
- use *append* to add elements to a /slice/
- *append* returns a new /slice/
- empty /slices/ default to nil
- use *make* to create a /slice/ with capacity

```go
var empty []int
withData := []int{0,1,2,3,4,5}

withData[1] = 5
x := withData[1] // 5

newSlice := withData[2:4] // => []int{2,3}
newSlice := withData[:2] // => []int{0,5}
newSlice := withData[2:] // => []int{2,3,4,5}
newSlice := withData[:] // => []int{0,5,2,3,4,5}

a := []int{1,3}
a = append(a, 4, 2)
// => []int{1,3,4,2}

var s []int // nil slice, preferred
s := []int{} // empty, non-nil slice

s := make([]int, 0, len(withData))
```

## Sorting
[source](https://gobyexample.com/sorting)

```go
package main

import (
    "fmt"
    "slices"
)

func main() {

    strs := []string{"c", "a", "b"}
    slices.Sort(strs)
    fmt.Println("Strings:", strs)

    ints := []int{7, 2, 4}
    slices.Sort(ints)
    fmt.Println("Ints:   ", ints)

    s := slices.IsSorted(ints)
    fmt.Println("Sorted: ", s)
}
```

## Sorting by Function
[source](https://gobyexample.com/sorting-by-functions)

```go
package main

import (
    "cmp"
    "fmt"
    "slices"
)

func main() {
    fruits := []string{"peach", "banana", "kiwi"}

    lenCmp := func(a, b string) int {
        return cmp.Compare(len(a), len(b))
    }

    slices.SortFunc(fruits, lenCmp)
    fmt.Println(fruits)

    type Person struct {
        name string
        age  int
    }

    people := []Person{
        Person{name: "Jax", age: 37},
        Person{name: "TJ", age: 25},
        Person{name: "Alex", age: 72},
    }

    slices.SortFunc(people,
        func(a, b Person) int {
            return cmp.Compare(a.age, b.age)
        })
    fmt.Println(people)
}
```
