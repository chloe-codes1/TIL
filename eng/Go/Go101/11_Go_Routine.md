# Go Routine

> Reference: [Go by example](https://gobyexample.com/goroutines), [A Tour of Go](https://tour.golang.org/concurrency/1), [Go Programming by Example](http://golang.site/go/article/21-Go-%EB%A3%A8%ED%8B%B4-goroutine)

<br>

<br>

### What is Go routines?

- **Lightweight thread** managed by Go runtime
- When calling a function using the **"go"** keyword in Go, runtime executes a new `goroutine`
- `goroutine` executes function routines **asynchronously**, so it's used to execute multiple codes **concurrently**

<br>

<br>

### Why Go routine?

- Created to implement **asynchronous concurrent processing** much lighter than OS Thread, basically managed by Go runtime itself
  - Multiple `goroutines`, which are work units managed on `Go runtime`, are executed as one OS Thread
    - That is, goroutines don't correspond 1:1 with OS Threads, but use much fewer OS Threads through **multiplexing**
    - In terms of memory, while OS Thread has a stack of 1MB, goroutine has a much smaller stack of a few KB
  - `Go runtime` manages goroutines and makes it easy to communicate between goroutines through **Go channels**

ex)

```go
package main
 
import (
    "fmt"
    "time"
)
 
func say(s string) {
    for i := 0; i < 10; i++ {
        fmt.Println(s, "---->", i)
    }
}
 
func main() {
    // 1. The Synchronous way
    say("Sync")
 
    // 2. Go routines
    go say("Async 1")
    go say("Async 2")
    go say("Async 3")
 
    // Sleep for 3 sec
    time.Sleep(time.Second * 3)
} 
