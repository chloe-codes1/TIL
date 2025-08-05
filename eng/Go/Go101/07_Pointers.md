# Pointers

> Let's learn about Go's pointers

<br>

<br>

Go allows you to do **low-level programming** with high-level code

<br>

## Check memory address and access that address

: Can be used when you don't want values to be copied

<br>

ex)

```go
package main

import "fmt"

func main() {
 a := 2
 b := a
 a = 10
  fmt.Println(a, b) // -> 10 2
}
```

- In the above example, you can see that the value is copied
  - That is, even if you update the value of a, the value of b does not change

<br>

However, when you want a **memory address** instead of copying the value, you can use the method below

<br>

<br>

### `&` operator

: You can use **&** to find the **address** of memory

```go
package main

import "fmt"

func main() {
 a := 2
 b := a
 a = 10
  fmt.Println(&a, &b) //-> 0xc0000160b0 0xc0000160b8
}
```

<br>

#### Accessing memory address using `&` operator

```go
package main

import "fmt"

func main() {
 a := 2
 b := &a
 a = 10
 fmt.Println(&a, b) // -> 0xc0000b4008 0xc0000b4008
}
```

- Here, by doing `b := &a`, b is looking at the memory of a
  - That's why the same memory address is output as above
- b is directly called a **pointer**

<br>

<br>

### `*` operator

: You can use ***** and addresses to look at the **value** of that memory address

```go
package main

import "fmt"

func main() {
 a := 2
 // get memory address
 b := &a
 a = 10
 fmt.Println(a, *b) // -> 10 10
}
```

<br>

- When dealing with very heavy data structures, using addresses stored in memory is efficient since you don't keep making copies
  - By utilizing pointers like this, you can make programs run fast!

<br>

#### Changing values through pointers

```go
package main

import (
 "fmt"
)

func main() {
 a := 2
 // get memory address
 b := &a
 a = 10

 // change object from address
 *b = 20
 fmt.Println(a, *b)
}
```

- You can change the value of a using **pointer** b that is connected to a's address 
