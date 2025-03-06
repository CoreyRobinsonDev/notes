
# HTTP Client
[source](https://gobyexample.com/http-client)


```go
    package main

    import (
        "bufio"
        "fmt"
        "net/http"
    )

    func main() {

        resp, err := http.Get("https://gobyexample.com")
        if err != nil {
            panic(err)
        }
        defer resp.Body.Close()

        fmt.Println("Response status:", resp.Status)

        scanner := bufio.NewScanner(resp.Body)
        for i := 0; scanner.Scan() && i < 5; i++ {
            fmt.Println(scanner.Text())
        }

        if err := scanner.Err(); err != nil {
            panic(err)
        }
    }
```

# HTTP Server
[source](https://gobyexample.com/http-server)

```go
    package main

    import (
        "fmt"
        "net/http"
    )

    func hello(w http.ResponseWriter, req *http.Request) {

        fmt.Fprintf(w, "hello\n")
    }

    func headers(w http.ResponseWriter, req *http.Request) {

        for name, headers := range req.Header {
            for _, h := range headers {
                fmt.Fprintf(w, "%v: %v\n", name, h)
            }
        }
    }

    func main() {

        http.HandleFunc("/hello", hello)
        http.HandleFunc("/headers", headers)

        http.ListenAndServe(":8090", nil)
    }
```

## URL Parsing
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

## Context
[source](https://gobyexample.com/context)

- a *context* carries dealines, cancellation signals, and other request scoped values across API boundaries

```go
    package main

    import (
        "fmt"
        "net/http"
        "time"
    )

    func hello(w http.ResponseWriter, req *http.Request) {

        ctx := req.Context()
        fmt.Println("server: hello handler started")
        defer fmt.Println("server: hello handler ended")

        select {
        case <-time.After(10 * time.Second):
            fmt.Fprintf(w, "hello\n")
        case <-ctx.Done():

            err := ctx.Err()
            fmt.Println("server:", err)
            internalError := http.StatusInternalServerError
            http.Error(w, err.Error(), internalError)
        }
    }

    func main() {

        http.HandleFunc("/hello", hello)
        http.ListenAndServe(":8090", nil)
    }
```
