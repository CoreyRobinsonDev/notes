
# Rate Limiting
[source](https://gobyexample.com/rate-limiting)

```go
package main

import (
    "fmt"
    "time"
)

func main() {
    requests := make(chan int, 5)
    for i := 1; i <= 5; i++ {
        requests <- i
    }
    close(requests)

    limiter := time.Tick(200 * time.Millisecond)

    for req := range requests {
        <-limiter
        fmt.Println("request", req, time.Now())
    }

    burstyLimiter := make(chan time.Time, 3)

    for i := 0; i < 3; i++ {
        burstyLimiter <- time.Now()
    }

    go func() {
        for t := range time.Tick(200 * time.Millisecond) {
            burstyLimiter <- t
        }
    }()

    burstyRequests := make(chan int, 5)
    for i := 1; i <= 5; i++ {
        burstyRequests <- i
    }
    close(burstyRequests)
    for req := range burstyRequests {
        <-burstyLimiter
        fmt.Println("request", req, time.Now())
    }
}
```

# URL Parsing
[source](https://gobyexample.com/url-parsing)

```go
    package main

    import (
        "fmt"
        "net"
        "net/url"
    )

    func main() {

        s := "postgres://user:pass@host.com:5432/path?k=v#f"

        u, err := url.Parse(s)
        if err != nil {
            panic(err)
        }

        fmt.Println(u.Scheme)

        fmt.Println(u.User)
        fmt.Println(u.User.Username())
        p, _ := u.User.Password()
        fmt.Println(p)

        fmt.Println(u.Host)
        host, port, _ := net.SplitHostPort(u.Host)
        fmt.Println(host)
        fmt.Println(port)

        fmt.Println(u.Path)
        fmt.Println(u.Fragment)

        fmt.Println(u.RawQuery)
        m, _ := url.ParseQuery(u.RawQuery)
        fmt.Println(m)
        fmt.Println(m["k"][0])
    }
```
