# If Statement
- if statements can include an initialization statement to be used within the block
- the comparison operators can be used to compare strings lexicographically

```go
num := 7
if v := 2 * num; v > 10 {
	fmt.Println(v)	
} else {
	fmt.Println(num)
}

"apple" < "banana" // true
"apple" > "banana" // false
```

# Switch Statement
- the value after the *switch* statement can be omitted and we can have boolean statements for each *case*

```go
operatingSystem := "windows"

switch operatingSystem {
case "windows": // do something
case "linux": // do something
case "macos": // do something
default: // do something
}

age := 21

switch {
case age > 20 && age < 30: // do something
case age == 10: // do something
default: // do something
}
```
