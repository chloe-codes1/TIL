# Getting Started With Go

> Go 를 공부해 보아요

<br>

<br>

## Go basic syntax

<br>

### 1. `println`, `print`

```go
package main
import "fmt"

func main() {
	fmt.Print("Hello goorm!")
}
```

- `fmt` package import 안해도 print / println 은 사용 가능

- **println** 과 **print** 는 line break 유무의 차이

  - **print**로 줄바꿈을 하려면 `\n` 사용하기!

- Single quote 안 됨!

  - Double quote 사용하기

- print 함수들은 함수 안에서의 연산 결과를 출력 할 수 있음!

  ex)

  ```go
  package main
  
  func main() {
    var num1 int = 1000
    var num2 int = 1413
  
    println("덧셈을 해보아요 ~ ", num1 + num2)
  }
  ```

  ```bash
  chloe@chloe-XPS-15-9570 ~/Workspace/Go/Go101
  $ ./calc
  덧셈을 해보아요 ~  2413
  ```

<br>

#### `fmt`  package

- 입출력을 위한 package
- 사용법
  - package main 밑줄에 `import "fmt"`  작성

<br>

<br>

### 2. Variables

<br>

#### 2-1 `:=`

- Short Assignment Statement 라고 불림
- type 선언 없이 변수 선언 가능
- **함수** 안에서만 사용 가능!!

