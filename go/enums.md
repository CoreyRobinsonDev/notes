# Enums
- *enums* are a sum type of a fixed number of values
- Go does not have an enum type as a language feature

```go
import "fmt"

type ServerState int // enum type has an underlying int type

// enum values are defined as consts
// keyword 'iota' generates successive constant values automatically (0,1,2,...)
const (
    StateIdle = iota
    StateConnected
    StateError
    StateRetrying
) 

// implementing the 'fmt.Stringer' interface allows the enum to be converted to strings
var stateName = map[ServerState]string {
    StateIdle:      "idle",
    StateConnected: "connected",
    StateError:     "error",
    StateRetrying:  "retrying"
}
func (s ServerState) String() string {
   return stateName[s] 
}
```
