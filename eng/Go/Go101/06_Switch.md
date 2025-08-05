# Switch

> Let's learn about Go's Switch

<br>

<br>

### Switch

: A way to check values

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

#### You can use switch to avoid rampant `if-else`, `else if` cases

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

#### You can also use `variable expression` in switch

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
