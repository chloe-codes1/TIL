# Maps

> Let's learn about Go's maps

<br>

<br>

### Map

- Map in Go is similar to **objects** in Python and JavaScript

  - Not exactly the same!

- To create a map, you must specify the `type` of **key** and **value**

  - `map[KEY_TYPE]VALUE_TYPE{}`

  - ex)

    ```go
    package main
    
    import "fmt"
    
    func main() {
     chloe := map[string]string{"name": "chloe", "age": "26"}
     fmt.Println(chloe) // -> map[age:26 name:chloe]
    }
    ```

    - In the above example, since we specified that we'll use **string** as value, putting integer 26 as the value for `age` will cause an error
    - To create an object with multiple types of values instead of just one type, you can use `struct`!

<br>

### Iterate over a Map using for loop

- You can traverse a Map using `for` and `range`

  - ex)

    ```go
    package main
    
    import "fmt"
    
    func main() {
     chloe := map[string]string{"name": "chloe", "age": "26"}
     for key, value := range chloe {
      fmt.Println(key, value)
     }
    }
    ``` 
