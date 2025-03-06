# Map

```go
foo := map[string]int{} // with map literal
foo := make(map[string]int) // with make function

foo["bar"] = 42
foo["bar"] = 73

baz, exists := foo["baz"]
// baz: 0; exists: false

delete(foo, "bar")
```
