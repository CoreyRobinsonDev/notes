# Time
[source](https://gobyexample.com/time)

## time.Parse()
- takes a string type
- returns a value of type *Time*
- the layout is set using values from this special timestamp `Mon Jan 2 15:04:05 -0700 MST 2006` 

```go
import "time"

func parseTime() time.Time {
    date := "Tue, 09/22/1995, 13:00"
    layout := "Mon, 01/02/2006, 15:04"

    t, err := time.Parse(layout, date) // time.Time, error
}
// => 1995-09-22 13:00:00 +0000 UTC
```
## time.Format()
- use *time.Format()* to format the structure of an existing *Time* value

```go
import (
    "fmt"
    "time"
)

func main() {
    t := time.Date(1995, time.September, 22, 13, 0, 0, 0, time.UTC)
    formattedTime := t.Format("Mon, 01/02/2006, 15:04")
    fmt.Println(formattedTime)
    // => Fri, 09/22/1995, 13:00
}
```
### Layout Options
| Time        | Options                    |
|-------------|----------------------------|
| Year        | 2006; 06                   |
| Month       | Jan; January; 01; 1        |
| Day         | 02; 2; _2(for preceding 0) |
| Weekday     | Mon; Monday                |
| Hour        | 15; 3; 03                  |
| Minute      | 04; 4                      |
| Second      | 05; 5                      |
| AM/PM Mark  | PM                         |
| Day of Year | 002; __2                   |


# Timers
[source](https://gobyexample.com/timers)

```go
package main

import (
    "fmt"
    "time"
)

func main() {

    timer1 := time.NewTimer(2 * time.Second)

    <-timer1.C
    fmt.Println("Timer 1 fired")

    timer2 := time.NewTimer(time.Second)
    go func() {
        <-timer2.C
        fmt.Println("Timer 2 fired")
    }()
    stop2 := timer2.Stop()
    if stop2 {
        fmt.Println("Timer 2 stopped")
    }

    time.Sleep(2 * time.Second)
}
```

# Tickers
[source](https://gobyexample.com/tickers)

```go
package main

import (
    "fmt"
    "time"
)

func main() {

    ticker := time.NewTicker(500 * time.Millisecond)
    done := make(chan bool)

    go func() {
        for {
            select {
            case <-done:
                return
            case t := <-ticker.C:
                fmt.Println("Tick at", t)
            }
        }
    }()

    time.Sleep(1600 * time.Millisecond)
    ticker.Stop()
    done <- true
    fmt.Println("Ticker stopped")
}
```
