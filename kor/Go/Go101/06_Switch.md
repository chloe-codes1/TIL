# Switch

> Go의 Switch에 대해 알아보아요

<br>

<br>

### Switch

: 값을 체크해주는 방법이다

ex)

```go
package main

import "fmt"

func canIDrink(age int) bool {
 switch age {
 case 18:
  return false
 case 19:
  return true
 }
 return false
}

func main() {
 fmt.Println(canIDrink(19))
}
```

<br>

#### switch를 활용하여 `if-else`, `else if` 를 난무하는 경우를 피할 수 있다

ex)

```go
package main

import "fmt"

// Avoid if else with switch
func canIDrive(age int) bool {
 switch {
 case age < 19:
  return false
 case age == 19:
  return true
 case age > 19:
  return true
 }
 return false
}

func main() {
 fmt.Println(canIDrive(18))
}
```

<br>

#### switch에서도 `variable expression` 을 사용할 수 있다

ex)

```go
package main

import "fmt"

// Variable expression in switch
func canIVote(age int) bool {
 switch koreanAge := age + 2; {
 case koreanAge < 19:
  return false
 case koreanAge == 19:
  return true
 case koreanAge > 19:
  return true
 }
 return false
}

func main() {
 fmt.Println(canIVote(29))
}
```
