# Structs

> 매력적인 struct에 대해 알아보아요

<br>

<br>

### Struct

- `Struct`는 **object**와 비슷하면서 **map** 보다 좀 더 유연한 것이 특징이다  

- **map** 은 지정한 type의 `Key`와 `Value`만 넣을 수 있지만, **struct**는 type에 상관없이 값을 넣을 수 있다

- `Struct`를 기본적으로 **structure(구조체)** 인데, struct를 만드는 방법은 아래와 같다

  1. 어떤 struct 인지 정의하고
  2. structure의 형태를 만들어 주면 된다

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

#### Struct의 값을 지정하기

1. 정의 된 순서대로 값을 지정하기

   ```go
   chloe := person{"chloe", 26, chloeFav}
   ```

   - 명확하게 어떤 value가 어떤 value인지 보이지 않기 때문에 좋지 않은 방법이다
     - 해당 값이 `struct`에서 몇번째인지 확인해야 하는 번거로움이 있다

2. 어떤 값인지 명시하여 지정하기

   ```go
   camila := person{name: "camila", age: 26, favFood: camilaFav}
   ```

- `struct` 를 비교하며 확인하지 않아도 되므로 명확하다

<br>

*단, 두 가지를 섞어서 사용할 수는 없다!*

<br>

#### Struct 활용하기

- Go는 Java 처럼 **class** 가 없고, Python이나 JavsScript처럼 **object**도 없다
  - `Struct`를 활용해야 한다!
- Struct로 **method** 도 만들 수 있다
- Go는 **construct method** 가 없다
  - Python의 `__init__`, JavaScript의 `constructor()` 같은 construct가 Go의 `struct`에는 없다
  - 직접 constructor를 만들어 실행해야 한다
- Go에서 거의 모든것을 `struct`를 활용하여 할 수 있으므로 struct는 중요한 역할을 한다!
