
# Spawning Processes
[source](https://gobyexample.com/spawning-processes)

- for spawning non go processes

```go
    package main

    import (
        "fmt"
        "io"
        "os/exec"
    )

    func main() {

        dateCmd := exec.Command("date")

        dateOut, err := dateCmd.Output()
        if err != nil {
            panic(err)
        }
        fmt.Println("> date")
        fmt.Println(string(dateOut))

        _, err = exec.Command("date", "-x").Output()
        if err != nil {
            switch e := err.(type) {
            case *exec.Error:
                fmt.Println("failed executing:", err)
            case *exec.ExitError:
                fmt.Println("command exit rc =", e.ExitCode())
            default:
                panic(err)
            }
        }

        grepCmd := exec.Command("grep", "hello")

        grepIn, _ := grepCmd.StdinPipe()
        grepOut, _ := grepCmd.StdoutPipe()
        grepCmd.Start()
        grepIn.Write([]byte("hello grep\ngoodbye grep"))
        grepIn.Close()
        grepBytes, _ := io.ReadAll(grepOut)
        grepCmd.Wait()

        fmt.Println("> grep hello")
        fmt.Println(string(grepBytes))

        lsCmd := exec.Command("bash", "-c", "ls -a -l -h")
        lsOut, err := lsCmd.Output()
        if err != nil {
            panic(err)
        }
        fmt.Println("> ls -a -l -h")
        fmt.Println(string(lsOut))
    }
```

# Executing Processes
[source](https://gobyexample.com/execing-processes)

```go
    package main

    import (
        "os"
        "os/exec"
        "syscall"
    )

    func main() {

        binary, lookErr := exec.LookPath("ls")
        if lookErr != nil {
            panic(lookErr)
        }

        args := []string{"ls", "-a", "-l", "-h"}

        env := os.Environ()

        execErr := syscall.Exec(binary, args, env)
        if execErr != nil {
            panic(execErr)
        }
    }
```
