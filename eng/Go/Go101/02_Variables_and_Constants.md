# Variables and Constants

> Declaration and initialization of variables/constants

<br>

<br>

## Before getting started

<br>

### Constants

- Variables that cannot change their values
  - **const** in Javascript!

#### Untype constant

- Constants without type

  - ex)

    ```go
    package main
    
    func main() {
     const name = "chloe"
    }
    ```

#### Type constant

- Constants with type

  - ex)

    ```go
    package main
    
    func main() {
      const name string = "chloe"
    }
    ```

- Of course, since it's a constant, you cannot change the value!

  - ex)

    ```go
    package main
    
    func main() {
      const name string = "chloe"
      name = "camila" // -> not possible
    }
    ```

<br>

### Variables

- Literally variables (values can be changed)
  - **let** in Javascript!

#### Untype variable

- Variables without type

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

- Variables with type

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

- Go tries to figure out the type of the value you wrote
  - Because Go is a **type language**!
    - Must tell what the *"Type is!"*
      - Like Java or typescript, you need to specify the type

<br>

<br>

## 1. Declaring variables

<br>

### 1-1. Variable declaration method in Go

#### `var variable_name variable_type`

- You can set initial values right where you declare the variable

  ex)

  ```go
  package main
  
  func main() {
    var num1 int = 1000
    var num2 int = 1413
  
    println("Let's do addition ~ ", num1 + num2)
  }
  ```

<br>

### 1-2. `:=`

- Called Short Assignment Statement

- Variable declaration possible **without type declaration**

  - Go finds the type for you!
    - Using this shorthand seems like it can be used flexibly like python!

- Can **only be used inside functions**!!

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

Be careful that Go generates an error if you create a variable and **don't use it**! 
