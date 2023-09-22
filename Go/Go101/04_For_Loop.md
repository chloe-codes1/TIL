# For Loop

> Go의 Loop를 알아보아요

<br>

<br>

### For

- Go의 looping은 오직 **for** loop 하나만 가능하다

<br>

### Range

- **slice**나 **map**에 loop를 적용할 수 있도록 해준다

  - range는 loop의 **index**와 **value**를 준다!

  - 단, **for** 안에서만 사용할 수 있다

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

- range를 활용하여 loop를 순회하면, 아래와 같이 두 개의 value를 return 한다
  1. index
  2. copy of the element at that index
- 만약 index가 필요 없고 값만 필요하다면, 위의 예시처럼 **ignored value**인 underscore (`_`) 를 사용하면 된다

<br>

`+`

range 를 사용한 for loop는 python 의 enumerate 와 유사하다!

<br>

#### Range를 사용하지 않은 for

- Range 없이도 for loop를 만들 수 있다

  - ex)

    ```go
    func add(numbers ...int) {
     for i := 0; i < len(numbers); i++ {
      fmt.Println(i)
     }
    }
    ```

- but, 코드가 길어지고 비효율적이므로 안 쓰게 될 것 같다!
