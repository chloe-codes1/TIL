# If Else

> Go의 conditonal statement를 알아보아요

<br>

<br>

### If

- 조건문을 표현할 때 if를 사용한다

  - ex)

    ```go
    package main
    
    import "fmt"
    
    func canIDrink(age int) bool {
     if age < 18 {
      return false
     }
     return true
    }
    
    func main() {
     fmt.Println(canIDrink(19))
    }
    
    ```

<br>

### Variable expression

- if를 사용하는 순간에 variable을 생성할 수 있다

  - if 바로 안쪽에서 variable을 생성하고, semicolon(`;`) 이후에 바로 해당 variable을 사용할 수 있다

  - ex)

    ```go
    package main
    
    import "fmt"
    
    func canIDrive(age int) bool {
     // create a variable right incide of the "if"
     if koreanAge := age + 2; koreanAge < 18 {
      return false
     }
     return true
    }
    
    func main() {
     fmt.Println(canIDrive(20))
    }
    ```

  - 이렇게 함으로써 Code를 읽는 다른 사람으로 하여금 *"if-else 조건에만 사용하기 위해 variable을 생성했구나!"* 를 알 수 있게 할 수 있다
