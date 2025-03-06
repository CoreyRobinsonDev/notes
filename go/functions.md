
# Functions
## Variadic Functions
```go
    func find (num int, nums...int) {}

    list := []int{1,2,3}
    find(1, list...)
```
## Named Return Values and Naked Return
- named return values are used with an empty return statement

```go
    func SumAndMultiplyThenMinus(a,b,c int) (sum, mult int) {
        sum, mult = a+b, a*b
        sum -= c
        mult -= c
        return
    }
```
## Pass by Value vs. Pass by Reference
- all arguments passed into a function are copied
- pass by reference to modify the underlying data

```go
    func HandlePointers(x,y *int) {}
```
