# Structs

> Let's learn about the attractive struct

<br>

<br>

### Struct

- `Struct` is similar to **object** but is more flexible than **map**

- **map** can only contain `Key` and `Value` of specified types, but **struct** can contain values regardless of type

- `Struct` is basically a **structure**, and the way to create a struct is as follows:

  1. Define what kind of struct it is
  2. Create the structure format

  - ex)

    ```go
    package main
    
    import "fmt"
    
    type person struct {
     name    string
     age     int
     favFood []string
    }
    
    func main() {
     favFood := []string{"guacamole", "omelet", "biscuits and gravy"}
     chloe := person{"chloe", 26, favFood}
     fmt.Println(chloe)
    }
    ```

<br>

#### Specifying values in Struct

1. Specify values in the defined order

   ```go
   chloe := person{"chloe", 26, chloeFav}
   ```

   - This is not a good method because it's not clear which value is which
     - There's the inconvenience of having to check what position the value is in the `struct`

2. Specify by clearly stating what value it is

   ```go
   camila := person{name: "camila", age: 26, favFood: camilaFav}
   ```

- It's clear since you don't need to compare and check the `struct`

<br>

*However, you cannot use the two methods mixed together!*

<br>

#### Using Struct

- Go doesn't have **class** like Java, and doesn't have **object** like Python or JavaScript
  - You must use `Struct`!
- You can also create **methods** with Struct
- Go doesn't have **construct method**
  - There's no construct like Python's `__init__`, JavaScript's `constructor()` in Go's `struct`
  - You must create and execute the constructor yourself
- Since you can do almost everything in Go using `struct`, struct plays an important role! 
