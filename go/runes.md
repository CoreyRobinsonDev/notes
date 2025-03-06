# Runes
- *rune* is an alias for *int32*
- the integer value stored in a *rune* represents a single unicode character

```go
import "fmt"

myRune := '¿'
fmt.Printf("myRune type: %T\n", myRune) // => "myRune type: int32"
fmt.Printf("myRune value: %v\n", myRune) // => "myRune value: 191"
fmt.Printf("myRune character: %c\n", myRune) // => "myRune character: ¿"
```
## Runes and Strings
- *strings* are UTF-8 encoded
- each charater of a a string can be 1,2,3 or 4 bytes
- slices of these characters can be iterated over by converting them into a slice of *runes*

```go

myString := "❗hello"
for index, char := range myString {
  fmt.Printf("Index: %d\tCharacter: %c\t\tCode Point: %U\n", index, char, char)
}
// =>
// Index: 0	Character: ❗		Code Point: U+2757
// Index: 3	Character: h		Code Point: U+0068
// Index: 4	Character: e		Code Point: U+0065
// Index: 5	Character: l		Code Point: U+006C
// Index: 6	Character: l		Code Point: U+006C
// Index: 7	Character: o		Code Point: U+006F
```

## Length
- use `len()` to get the number of bytes
- use `utf8.RuneCountInString()` to get the number of runes

```go
import "unicode/utf8"
import "fmt"

myString := "❗hello"

fmt.Printf(
    "myString - Length: %d - Runes: %d\n",
    len(myString),
    utf8.RuneCountInString(myString)
) // => myString - Length: 8 - Runes: 6
```
