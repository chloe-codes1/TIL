# Variables and Constants

> 변수/상수의 선언과 초기화

<br>

<br>

## Before getting started

<br>

### Constants

- 변수지만 값을 바꿀 수 없는 것
  - Javascript에서는 **const**!

#### Untype constant

- 타입이 없는 상수

  - ex)

    ```go
    package main
    
    func main() {
     const name = "chloe"
    }
    ```

#### Type constant

- 타입이 있는 상수

  - ex)

    ```go
    package main
    
    func main() {
      const name string = "chloe"
    }
    ```

- 당연하지만 상수이므로 값을 변경할 수 없다!

  - ex)

    ```go
    package main
    
    func main() {
      const name string = "chloe"
      name = "camila" // -> 불가
    }
    ```

<br>

### Variables

- 말 그대로 변수 (값을 변경할 수 있다)
  - Javascript에서는 **let**!

#### Untype variable

- 타입이 없는 변수

  - ex)

    ```go
    package main
    
    import "fmt"
    
    func main() {
    
     var year = 2020
     fmt.Println(year)
    
    }
    ```

#### Type variable

- 타입이 있는 변수

  - ex)

    ```go
    package main
    
    import "fmt"
    
    func main() {
    
     var month int = 12
     // -> month := 12 (same)
    
     fmt.Println(month)
    }
    ```

<br>

### Types in Go

- Go는 작성한 값의 type을 알아내려고 한다
  - Go는 **type langague** 이기 때문!
    - *"Type이 무엇이다!"* 라는 것을 알려주어야 함
      - Java나 typescript 처럼 타입을 알려줘야함

<br>

<br>

## 1. 변수 선언하기

<br>

### 1-1. Go에서의 변수 선언 방식

#### `var 변수이름 변수형`

- 변수를 선언한 곳에서 바로 초기값을 설정할 수 있음

  ex)

  ```go
  package main
  
  func main() {
    var num1 int = 1000
    var num2 int = 1413
  
    println("덧셈을 해보아요 ~ ", num1 + num2)
  }
  ```

<br>

### 1-2. `:=`

- Short Assignment Statement 라고 불림

- **type 선언 없이** 변수 선언 가능

  - Go가 type을 찾아준다!
    - 이렇게 shorthand 사용하면 python처럼 유연하게 사용 가능할듯!

- **함수** 안에서만 사용 가능!!

  ex)

  ```go
  package main
  
  func main() {
   var a int = 100
   var b string = "Haha"
   c := 200
   print(b, a+c);
  }
  ```

<br>

<br>`+`

Go는 변수를 만들고 **사용하지 않으면** 에러를 발생시키므로 유의하자!
