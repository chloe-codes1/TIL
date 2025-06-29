# Arrays and Slices

> Go의 array와 slice에 대해 알아보아요

<br>

<br>

### Arrays

- Go에서는 array를 만들때에는 해당 array의 **length**를 명시해 주어야 한다

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

    - Go의 **index**는 **0**부터 시작하므로 위의 예시에서 names[4]는 5번째 index이다

  - array를 생성할 때 **명시한 길이**보다 큰 index를 넣으면 **errorr**가 발생한다

<br>

<br>

### Slices

- Array의 크기를 제한하고 싶을 때도 있지만, array의 **크기에 제한 없이** element를 추가 하고 싶을 때도 있을 것이다

  - 그럴 때 쓸 수 있는 data type이 **slice** 이다

- Go에서의 slice는 array인데 **length**가 없는 것이다

  - ex)

    ```go
    package main
    
    import "fmt"
    
    func main() {
     states := []string{"Florida", "Kentucky"}
     fmt.Println(states)
    }
    ```

    - array와의 차이점은 **length**가 없다는 것 뿐이다

<br>

#### append()

- Slice에 **item**을 **추가**할 때에는 `append()` function을 사용한다
- append()는 두 개의 argument를 갖는다
  1. **slice**
  2. **value**

- 하지만 `append()`는 **slice** 를 수정하지는 않는다

  - `append()` 새로운 값이 추가된 slice를 **return** 한다!

    - 그러므로 해당 slice에 다시 update 해줘야 한다

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

*아마 대부분 slice를 사용하게 될 것 같다!*
