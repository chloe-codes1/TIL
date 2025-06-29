# Go Routine

> Reference: [Go by example](https://gobyexample.com/goroutines), [A Tour of Go](https://tour.golang.org/concurrency/1), [예제로 배우는 Go 프로그래밍](http://golang.site/go/article/21-Go-%EB%A3%A8%ED%8B%B4-goroutine)

<br>

<br>

### What is Go routines?

- Go runtime이 관리하는 **Lightweight thread**
- Go에서 **"go"** keyword를 사용하여 함수를 호출하면, runtime 시 새로운 `goroutine` 을 실행한다
- `goroutine`은 **비동기적(asynchronously)** 으로 함수 routine을 실행하기 때문에 여러 code를 **동시에 (concurrently)** 실행하는데 사용된다

<br>

<br>

### Why Go routine?

- OS Thread 보다 훨씬 가볍게 **비동기 concurrent 처리**를 구현하기 위하여 만든 것으로, 기본적으로 Go runtime이 자체 관리한다
  - `Go runtime` 상에서 관리되는 작업 단위인 여러 `goroutine` 들은 하나의 OS Thread로 실행된다
    - 즉, goroutine들은 OS Thrad와 1:1로 대응되지 않고, **multiplexing**으로 훨씬 적은 OS Thread를 사용한다
    - Memory 측면에서도 OS Thread가 1MB의 stack을 갖는 반면, goroutine은 이보다 훨씬 작은 몇 KB의 stack을 갖는다
  - `Go runtime`은 goroutine을 관리하면서 **Go channel**을 통해 goroutine 간의 통신을 쉽게 할 수 있도록 한다

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
```

 

