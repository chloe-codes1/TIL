# Pointers

> Go의 pointer에 대해 알아보아요

<br>

<br>

Go는 높은 수준의 code로 **low-level programming** 을 할 수 있도록 해준다

<br>

## 메모리 주소를 확인하고 해당 주소에 접근 하기

: 값이 복사 되는 것을 원치 않을 때 활용할 수 있다

<br>

ex)

```go
package main

import "fmt"

func main() {
 a := 2
 b := a
 a = 10
  fmt.Println(a, b) // -> 10 2
}
```

- 위의 예시에서 값이 복사되는 것을 확인 할 수 있다
  - 즉, a의 값을 update 해도 b의 값은 변하지 않는다

<br>

하지만 값을 복사하는 것이 아닌, **메모리 주소**를 원할 때에는 아래의 방법을 사용하면 된다

<br>

<br>

### `&` operator

: **&** 를 사용하여 memory의 **주소**를 알아낼 수 있다

```go
package main

import "fmt"

func main() {
 a := 2
 b := a
 a = 10
  fmt.Println(&a, &b) //-> 0xc0000160b0 0xc0000160b8
}
```

<br>

#### `&` operator를 사용하여 메모리 주소에 접근하기

```go
package main

import "fmt"

func main() {
 a := 2
 b := &a
 a = 10
 fmt.Println(&a, b) // -> 0xc0000b4008 0xc0000b4008
}
```

- 여기서 `b := &a` 를 함으로써 b는 a의 메모리를 보고있게 된다
  - 그렇기 때문에 위와 같이 같은 메모리 주소가 출력된다
- b를 바로 **pointer** 라고 한다

<br>

<br>

### `*` operator

: ***** 와 주소를 사용하여 해당 메모리 주소의**값**을 살펴볼 수 있다

```go
package main

import "fmt"

func main() {
 a := 2
 // get memory address
 b := &a
 a = 10
 fmt.Println(a, *b) // -> 10 10
}
```

<br>

- 아주 무거운 data structure 다룰 때 메모리에 저장된 주소를 활용하는 것이 계속해서 복사본을 만들지 않으므로 효율적이다
  - 이렇게 pointer를 활용함으로써 program을 빠르게 동작하도록 할 수 있다!

<br>

#### pointer를 통해 값을 변경하기

```go
package main

import (
 "fmt"
)

func main() {
 a := 2
 // get memory address
 b := &a
 a = 10

 // change object from address
 *b = 20
 fmt.Println(a, *b)
}
```

- a의 주소와 연결되어 있는 **pointer** b를 이용해서 a의 값을 변경할 수 있다
