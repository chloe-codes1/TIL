# For Loop

> Let's learn about Go's Loop

<br>

<br>

### For

- Go's looping is only possible with **for** loop

<br>

### Range

- Allows you to apply loops to **slice** or **map**

  - range gives you the **index** and **value** of the loop!

  - However, it can only be used inside **for**

  - ex)

    ```go
    package main
    
    import "fmt"
    
    func addAll(numbers ...int) int {
     total := 0
     // for loop w/ range
     for _, number := range numbers {
      total += number
     }
     return total
    }
    
    func main() {
     total := addAll(1, 2, 3, 4, 5, 6, 7, 8, 9)
     fmt.Println(total)
    }
    
    ```

- When traversing a loop using range, it returns two values as follows:
  1. index
  2. copy of the element at that index
- If you don't need the index and only need the value, you can use the **ignored value** underscore (`_`) as in the example above

<br>

`+`

for loop using range is similar to python's enumerate!

<br>

#### For without Range

- You can create for loops without range

  - ex)

    ```go
    func add(numbers ...int) {
     for i := 0; i < len(numbers); i++ {
      fmt.Println(i)
     }
    }
    ```

- but, since the code gets longer and inefficient, I don't think I'll use it! 
