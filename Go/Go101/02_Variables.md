# Variables in Go

> 변수의 선언과 초기화

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

- type 선언 없이 변수 선언 가능

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

  

