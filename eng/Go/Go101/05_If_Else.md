# If Else

> Let's learn about Go's conditional statement

<br>

<br>

### If

- Use if to express conditional statements

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

- You can create a variable at the moment you use if

  - You can create a variable right inside the if, and use that variable right after the semicolon(`;`)

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

  - By doing this, you can let other people reading the code know that *"the variable was created only for use in if-else conditions!"*
