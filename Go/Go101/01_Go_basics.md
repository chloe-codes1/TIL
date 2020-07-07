# Getting Started With Go

> Go 를 공부해 보아요
>
> *A huge thank you to [Calvin](https://github.com/kcalvinalvin)!*

<br>

<br>

## Install Go on Ubuntu

<br>

### 1. Go 1.14 설치하기

- `longsleep/golang-backports` PPA 를 사용하여 설치

  ``` bash
  $ sudo add-apt-repository ppa:longsleep/golang-backports
  $ sudo apt update
  $ sudo apt install golang-go
  ```

<br>

### 2. environment variable 설정

- Go는 2개의 environment variable을 갖고 있다 - `GOPATH` & `GOROOT` 
- `GOROOT`
  - **Go** binaries가 위치한 곳
  - `sudo apt install golang-go`로 설치하면 **Go** 를 default path에 설치하므로 따로 수정할 필요 없다!
- `GOPATH`
  - user **go** envirionment path
  - project file들이 위치한 곳을 설정해야 함
  - `go import` 로 package들을 import 할 때 `GOPATH` 로 불러옴
  - 일반적으로 `$HOME/go` 에 `GOPATH` 를 설정함
    - `go install` 이나 `go import` 를 할 때 **go** 는 `GOPATH` 를 찾게 되므로 중요하다!

<br>

> GOPATH 설정

``` bash
$ export GOPATH=$HOME/go
```

> PATH 설정

```bash
$ export PATH=$PATH:$GOPATH/bin
```

<br>

### 4. Go version 확인하기

```bash
chloe@chloe-XPS-15-9570 ~
$ go version
go version go1.14.2 linux/amd64
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

## Why Go?

- **Go**는 **간단하고 간결한 직관적인 언어** 를 지향함
  - `OOP` 를 지원한다
    - class, 객체, 상속의 개념이 없다
  - **Go**에서 쓰이는 **키워드**는 Java의 절반 수준인 25개 밖에 되지 않음
    - 간단!
  - Complie 언어지만 compiler의 속도가 매우 빠르기 때문에 interpreter 언어처럼 쓸 수 있음

- 좋은 **build system** 을 갖고 있음
  - build 속도가 매우 빠름
    - 몇 천줄의 코드로 이루어진 프로젝트도 단 몇 초만에 complie 한다!
  - `Code import` 가 off url import 기반이다
    - 그래서 dependency를 관리하기 좋다!
      - **Go module**은 import 시에 url을 hash 할 수 있게 해준다
        - 다른 build system에서 .lock file 을 import 하는 것과 유사함!

<br>

<br>

## 콘솔 출력 함수 - `println`, `print`

> 출력 해보기

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

<br>

`+`

### Useful Go resources recommended by Calvini

- gobyexample.com
- tour.golang.org
- blog.golang.org
- dave.cheney.net
- https://golang.org/doc/effective_go.html
  - must read!