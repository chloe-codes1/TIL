# Getting Started With Go

> Let's study Go
>
> *A huge thank you to [Calvin](https://github.com/kcalvinalvin)!*

<br>

<br>

## What is Go Language?

- Programming language developed by Google
- Syntax is similar to C language, but designed to handle **Concurrency programming** easily
  - `Concurrency programming`
    - Means that the program can do other things first while performing relatively time-consuming operations such as DB requests or network communication like web services
- Although it's a relatively recently emerged programming language, it's **not complex and a practical language**
- Representative projects that utilize **Go** include `Docker` and `Kubernetes`

<br>

<br>

## Why Go?

- **Go** aims for a **simple, concise, and intuitive language**
  - Supports `OOP`
    - No concepts of class, objects, inheritance
  - **Keywords** used in **Go** are only 25, half the level of Java
    - Simple!
  - Although it's a compiled language, the compiler speed is very fast, so it can be used like an interpreter language

- Has a good **build system**
  - Build speed is very fast
    - Projects consisting of thousands of lines of code compile in just a few seconds!
  - `Code import` is based on off url import
    - So it's good for managing dependencies!
      - **Go module** allows you to hash URLs when importing
        - Similar to importing .lock files in other build systems!

<br>

<br>

## Install Go on Ubuntu/Mac

<br>

### 1. Install Go 1.14

#### Ubuntu

- Install using `longsleep/golang-backports` PPA

  ``` bash
  sudo add-apt-repository ppa:longsleep/golang-backports
  sudo apt update
  sudo apt install golang-go
  ```

#### MacOS

- Download & install package from [golang.org](https://golang.org/doc/install)

<br>

### 2. Check Go version

#### Ubuntu

```bash
chloe@chloe-XPS-15-9570 ~
$ go version
go version go1.14.2 linux/amd64
```

#### MacOS

```bash
~ via ⬢ v14.15.1
➜ go version
go version go1.15.6 darwin/amd64
```

<br>

### 3. Workspace setup

- Create a directory to proceed with Go projects
  - ex) `/Users/chloe/workspace/go`
- Create 3 directories inside that directory as follows
  - **bin**
    - Where OS-specific executable binary files are stored after source code is compiled
  - **pkg**
    - Where library files are stored after packages needed for the project are compiled
  - **src**
    - Where written source code and open source codes are stored

<br>

### 4. Environment variable setup

- Go has 2 environment variables - `GOPATH` & `GOROOT`
- `GOROOT`
  - Where **Go** binaries are located
  - If you install with `sudo apt install golang-go`, **Go** is installed in the default path, so no need to modify separately!
    - On Mac, it's installed in `/usr/local/go`
- `GOPATH`
  - User **go** environment path
  - Need to set where project files are located
  - When importing packages with `go import`, it's loaded from `GOPATH`
  - Generally set `GOPATH` to `$HOME/go`
    - Important because when doing `go install` or `go import`, **go** looks for `GOPATH`!

<br>

#### 4-1. Ubuntu $GOPATH setup

> GOPATH setup

``` bash
export GOPATH=$HOME/go
```

> PATH setup

```bash
export PATH=$PATH:$GOPATH/bin
```

<br>

#### 4-2. MacOS $GOPATH setup

> Add the following to `~/.zshrc`

```bash
export GOPATH="/Users/chloe/workspace/go"
export PATH="$GOPATH:$PATH"
```

<br>

`+`

After setting **$GOPATH**, you can use the `go env` command to check if it's properly applied!

<br>

### 5. `src` in $GOPATH

- Go downloads and stores downloaded codes in `$GOPATH/src` **classified** by downloaded **domain**
  - ex) github.com, golang.org, google-golang.org, etc.
  - For source code I write, I'll create a directory with github user name inside github.com

<br>

<br>

## Getting started with Go

<br>

### 1. Main package

- Naming the package **main.go** means you will **compile** this project and use it

  - That is, all packages except **main.go** are not compiled!

- Since **main** is the entry point, the compiler looks for packages named main first

  - ex) `package main`

- Go looks for a function called **func main() {}**

  - This is the **entrypoint** of the Go program!

- Automatically, the compiler first finds and executes the **main package** and the **main function** inside it

  - ex)

    > main.go

    ```go
    package main
    
    import "fmt"
    
    func main() {
     fmt.Println("Hello World")
    }
    ```

<br>

### 2. Packages and imports

- To **export** a function in Go, write it in **upper-case**

  - ex)

    > something.go

    ```go
    package something
    
    import "fmt"
    
    func saySeeya() {
     fmt.Println("See ya!")
    }
    
    func SayHello() {
     fmt.Println("Hello!")
    }
    ```

    > main.go

    ```go
    package main
    
    import (
     "fmt"
    
     "github.com/chloe-codes1/go101/something"
    )
    
    func main() {
     fmt.Println("Hello World")
     something.SayHello()
    }
    ```

<br>

<br>

## Console output functions - `println`, `print`

> Let's output

ex)

```go
package main
import "fmt"

func main() {
 fmt.Print("Hello goorm!")
}
```

- print / println can be used without importing `fmt` package

- **println** and **print** differ in the presence of line break

  - To make a line break with **print**, use `\n`!

- Single quotes don't work!

  - Use double quotes

- print functions can output the results of operations inside functions!

  ex)

  ```go
  package main
  
  func main() {
    var num1 int = 1000
    var num2 int = 1413
  
    println("Let's do addition ~ ", num1 + num2)
  }
  ```

  ```bash
  chloe@chloe-XPS-15-9570 ~/Workspace/Go/Go101
  $ ./calc
  Let's do addition ~  2413
  ```

<br>

#### `fmt` package

- Package for input/output
- How to use
  - Write `import "fmt"` below package main

<br>

<br>

<br>

`+`

### Useful Go resources recommended by Calvini

- gobyexample.com
- tour.golang.org
- blog.golang.org
- dave.cheney.net
- <https://golang.org/doc/effective_go.html>
  - must read! 
