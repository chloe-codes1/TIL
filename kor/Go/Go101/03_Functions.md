# Functions

> Go의 functions를 알아보아요

<br>

<br>

### Types in fuction

- 함수의 **argument**와 **return 값**의 type을 **명시**해줘야 한다

  - compiler에게 type이 무엇인지 알려줌으로써 빠르게 compile 할 수 있게 한다!

    - Java랑 유사! Python이랑은 너무 다름...

  - ex)

    ```go
    package main
    
    import "fmt"
    
    func multiply(a int, b int) int {
     return a * b
    }
    
    func main() {
     fmt.Println(multiply(2, 4))
    }
    ```

- argument 들의 **type이 같으면** 한 번만 명시해도 된다

  - ex)

    ```go
    func multiply(a, b int) int {
     return a * b
    }
    ```

- **return이 필요한 함수**는 꼭 return type을 명시해야 한다!

<br>

### Multiple Return Values

- Go는 multiple return value 를 지원한다

  - 많은 프로그래밍 언어들과 다른 Go의 특징이다!

  - ex)

    ```go
    package main
    
    import (
     "fmt"
     "strings"
    )
    
    func lenAndUpper(name string) (int, string) {
     return len(name), strings.ToUpper(name)
    }
    
    func main() {
     totalLength, upperName := lenAndUpper("chloe")
     fmt.Println(totalLength, upperName)
    }
    
    ```

- 단, return 하는 개수보다 적게 값을 받을 수 없다!

  - ex) Error가 발생할 예시

    ```go
     totalLength := lenAndUpper("chloe")
    ```

    - lenAndUpper는 두 개의 값을 return 하기 때문에 아래와 같은 error를 뱉는다

      ```bash
      go101/03_functions on  master [!?] via 🐹 v1.15.6 
      ➜ go run main.go
      # command-line-arguments
      ./main.go:18:14: assignment mismatch: 1 variable but lenAndUpper returns 2 values
      ```

- 이럴 때에는 `_` 를 넣어 value 값을 무시하도록 하면 된다

  - ex)

    ```go
     totalLength, _ := lenAndUpper("chloe")
    ```

    - 이렇게 `underscore (_)` 는 **ignored value**로 사용할 수 있다!
      - compiler는 ignored value를 말그대로 무시한다

<br>

### Variadic functions

- `...` 을 사용하여 가변인자 함수를 만들 수 있다

  - 방법은 type앞에 `...` 를 붙이면 된다! 이게 끝이다!

  - ex)

    ```go
    func repeatMe(words ...string) {
     fmt.Println(words)
    }
    ```

<br>

### Naked returns

- 함수의 return type을 명시할 때 return할 값을 **미리 선언**하고, 비어있는 return을 하는 것

  - 선언 할 때 초기화 되므로 함수 내부에서는 해당 variable을 update 하는 것이다!

    - return할 value를 명시하지 않고 **return** 할 수 있다

  - ex)

    ```go
    package main
    
    import (
     "fmt"
     "strings"
    )
    
    func lenAndLower(name string) (length int, lowercase string) {
     length = len(name)
     lowercase = strings.ToLower(name)
     return
    }
    
    func main() {
     length, name := lenAndLower("CHLOE")
     fmt.Println(length, name)
    }
    ```

- 확실하게 어떤 값이 return 되는지 명시하고 싶으면 사용하지 않는 것이 좋다

<br>

### defer

- function이 끝난 후 실행되는 코드

  - 함수가 종료되었을 때 **defer**를 통해 추가적으로 무언가 동작할 수 있도록 설정할 수 있다

    - return 값이 있는 함수라면 return 된 후에 **defer** 가 실행된다

  - ex)

    ```go
    func lenAndLower(name string) (length int, lowercase string) {
      // defer
     defer fmt.Println("Done!")
      
     length = len(name)
     lowercase = strings.ToLower(name)
     return
    }
    ```

- defer를 함수 종료 후 image나 file을 닫거나 삭제하고, API request 보내는 것에 활용할 수 있다!
