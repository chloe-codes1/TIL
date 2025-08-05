# Arrays and Slices

> Let's learn about Go's arrays and slices

<br>

<br>

### Arrays

- In Go, when creating an array, you must specify the **length** of that array

  - ex)

    ```go
    package main
    
    import "fmt"
    
    func main() {
     names := [5]string{"chloe", "camila", "bella"}
     names[3] = "charlotte"
     names[4] = "bree"
     fmt.Print(names)
    }
    ```

    - Go's **index** starts from **0**, so in the above example, names[4] is the 5th index

  - If you put an index larger than the **specified length** when creating an array, an **error** will occur

<br>

<br>

### Slices

- Sometimes you want to limit the size of an array, but sometimes you want to add elements **without size limitation**

  - The data type you can use in such cases is **slice**

- Slice in Go is an array but **without length**

  - ex)

    ```go
    package main
    
    import "fmt"
    
    func main() {
     states := []string{"Florida", "Kentucky"}
     fmt.Println(states)
    }
    ```

    - The only difference from array is that there's no **length**

<br>

#### append()

- When **adding** **items** to a slice, use the `append()` function
- append() takes two arguments:
  1. **slice**
  2. **value**

- However, `append()` does not modify the **slice**

  - `append()` **returns** a slice with new values added!

    - So you need to update the slice again

    - ex)

      ```go
      package main
      
      import "fmt"
      
      func main() {
       states := []string{"Florida", "Kentucky"}
       states = append(states, "California")
       fmt.Println(states)
      }
      ```

<br>

*I think I'll probably use slice most of the time!* 
