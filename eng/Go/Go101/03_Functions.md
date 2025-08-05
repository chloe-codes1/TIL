# Functions

> Let's learn about Go's functions

<br>

<br>

### Types in function

- You must **specify** the type of function's **arguments** and **return values**

  - By telling the compiler what type it is, you can compile quickly!

    - Similar to Java! Very different from Python...

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

- If arguments have the **same type**, you only need to specify once

  - ex)

    ```go
    func multiply(a, b int) int {
     return a * b
    }
    ```

- **Functions that need return** must specify return type!

<br>

### Multiple Return Values

- Go supports multiple return values

  - A characteristic of Go that's different from many programming languages!

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

- However, you cannot receive fewer values than the number of returns!

  - ex) Example that will cause an error

    ```go
     totalLength := lenAndUpper("chloe")
    ```

    - Since lenAndUpper returns two values, it produces the following error

      ```bash
      go101/03_functions on  master [!?] via 🐹 v1.15.6 
      ➜ go run main.go
      # command-line-arguments
      ./main.go:18:14: assignment mismatch: 1 variable but lenAndUpper returns 2 values
      ```

- In this case, you can put `_` to ignore the value

  - ex)

    ```go
     totalLength, _ := lenAndUpper("chloe")
    ```

    - This way `underscore (_)` can be used as **ignored value**!
      - The compiler literally ignores ignored values

<br>

### Variadic functions

- You can create variadic functions using `...`

  - The method is to put `...` before the type! That's it!

  - ex)

    ```go
    func repeatMe(words ...string) {
     fmt.Println(words)
    }
    ```

<br>

### Naked returns

- When specifying the return type of a function, **pre-declare** the values to return and make an empty return

  - Since it's initialized when declared, inside the function you're updating that variable!

    - You can **return** without specifying the return value

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

- If you want to clearly specify what value is returned, it's better not to use this

<br>

### defer

- Code that executes after the function ends

  - You can set something to operate additionally through **defer** when the function terminates

    - If it's a function with a return value, **defer** executes after return

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

- You can use defer to close or delete images or files after function termination, and send API requests! 
