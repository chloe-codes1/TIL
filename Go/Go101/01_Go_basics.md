# Getting Started With Go

> Go 를 공부해 보아요
>
> [한 눈에 끝내는 고랭 기초]([https://edu.goorm.io/lecture/2010/%25ED%2595%259C-%25EB%2588%2588%25EC%2597%2590-%25EB%2581%259D%25EB%2582%25B4%25EB%258A%2594-%25EA%25B3%25A0%25EB%259E%25AD-%25EA%25B8%25B0%25EC%25B4%2588](https://edu.goorm.io/lecture/2010/%ED%95%9C-%EB%88%88%EC%97%90-%EB%81%9D%EB%82%B4%EB%8A%94-%EA%B3%A0%EB%9E%AD-%EA%B8%B0%EC%B4%88))

<br>

<br>

## Install Go on Ubuntu

<br>

### 1. Linux용으로 다운로드

- [공식 사이트](https://golang.org/dl/)에서 최신 버전인 `1.14.linux-amd64.tar.gz` 로 설치함

<br>

### 2. `/usr/local` 로 tar.gz file 옮기기

``` bash
$ tar -C /usr/local -xzf go$VERSION.$OS-$ARCH.tar.gz
```

<br>

### 3. PATH environment variable 설정

```bash
$ export PATH=$PATH:/usr/local/go/bin
```

<br>

### 4. Go version 확인하기

```bash
chloe@chloe-XPS-15-9570 ~
$ go version
go version go1.14.4 linux/amd64
```

<br>

<br>

## What is Go Language?

- Google이 개발한 programming language
- 문법은 C언어와 유사하지만, 동시성 (Concurrency) programming을 다루기 편하도록 설계됨
  - `동시성 프로그래밍`
    - web service와 같이  DB요청이나 Network 통신과 같이 비교적 시간이 많이 걸리는 연산을 하는 동안 프로그램이 다른 이를 먼저할 수 있도록 함을 의미
- 비교적 최근에 등장한 프로그래밍 언어이지만 비교적 **복잡하지 않고 실용적인 언어**임
- **Go**를 활용하는 대표적인 프로젝트는 `Docker`와 `Kubernetes` 가 있음

<br>

<br>

## 콘솔 출력 함수 - `println`, `print`

ex)

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