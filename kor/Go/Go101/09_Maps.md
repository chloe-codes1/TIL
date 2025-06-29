# Maps

> Go의 map에 대해 알아보아요

<br>

<br>

### Map

- Go에서의 map은 Python과 JavaScript의 **object**와 비슷하다

  - 완전히 같지는 않다!

- map을 만들기 위해서는 **key**와 **value**의 `type`을 명시해야 한다

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

    - 위의 예시에서 value로 **string**을 사용할 것이라고 명시했으므로, `age`의 value 값으로 integer 26을 넣으면 error가 발생한다
    - value의 type 한 가지가 아닌 여러가지 type을 가진 object를 만들려면 `struct` 구조체를 를 사용하면 된다!

<br>

### Iterate over a Map using for loop

- `for` 와 `range` 를 사용하여 Map을 순회 할 수 있다

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
