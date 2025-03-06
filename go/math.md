# Rand
```go
import "math/rand"

n := rand.Intn(100) // => 0 <= n < 100
f := rand.Float64() // => 0.0 <= f < 1.0

x := []string{"a","b","c","d","e"}
rand.Shuffle(len(x), func(i, j int) {
    x[i], x[j] = x[j], x[i]
})
```
