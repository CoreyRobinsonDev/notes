# Packages
- all source files in a directory must share the same package name
- private identifiers use *camelCase*
- public identifiers use *PascalCase*

```go
package lasagna
```

# Variables
- mutable by default
- Go is statically typed
- variables can be assigned values after declared

```go
	var num int 	// Explicitly typed
	num := 10 		// Implicitly typed as an int

	count := 1 		// Assign initial value
	count = 2 		// Update to new value
	count = false 	// compiler error
```

## Constants
- immutable by default

```go
	const Age = 21
```

# Functions
```go
	package greeting

	func Hello (name string) string {
		return hi(name)
	}

	func hi (name string) string {
		return "hi " + name
	}
```
# Comments
- use the *godoc* command to extract comments for package documentation
- documentation comments should start with the name of the thing

```go
	// Package kelvin provides tools to convert
	// temperatures to and from Kelvin
	package kelvin

	// TemperatureCelsius represents a certain temperature in degrees
	var TemperatureCelsius float64

	// CelsiusFreezingTemp returns an integer value equal to the temperature at which water freezes in degrees Celsius
	func CelsiusFreezingTemp() int {
		return 0
	}
``` 
	

