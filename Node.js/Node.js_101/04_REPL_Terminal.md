# REPL Terminal

<br>

<br>

### REPL (Read Eval Print Loop)

> Window command, UNIX/LINUX Shell 처럼 사용자가 command를 입력하면 system이 값을 반환하는 환경을 가리킴

<br>

Node.js는 REPL 환경과 함께 제공되며, 다음과 같은 기능을 수행 할 수 있다

- **Read**

  : User의 값을 입력 받아 JavaScript data 구조로 memory에 저장함

- **Eval**

  : 데이터를 처리 (Evaluate) 함

- **Print**

  : 결과값을 출력함

- **Loop**

  : Read, Eval, Print를 유저가 `ctrl + c` 를 두 번 눌러 종료할 때 까지 반복함

<br>

*Node.js의 REPL 환경은 JavaScript code를 testing & debugging 할 때 유용하게 사용됨!*

<br>

<br>

### Starting REPL

<br>

> REPL은 Shell / Console에 parameter 없이 node를 실행하여 시작할 수 있음

```bash
$ node
>
```

<br>

#### 1. 간단한 표현식 사용

<br>

```shell
$ node
> 1 + 5
6
> 1 + ( 6 / 2 ) - 3
1
>
```

<br>

<br>

#### 2. 변수 사용

- 다른 script 처럼, 변수에 값을 저장하고 나중에 다시 출력 할 수 있음
- `var` keyword를 사용하면
- 명령어를 입력했을 때 변수의 값이 출력되지 않고,
- `var` keyword를 사용하지 않으면
  - 변수의 값이 출력 됨
- **console.log()**를 통해 출력 할 수 있음

<br>

```shell
$ node
> x = 10
10
> var y = 5
undefined
> x + y
15
> console.log("Value is " + ( x + y ))
Value is 15
undefined
```

<br>

<br>

#### 3. Multi-line Expression 사용

<br>

> do-while loop REPL에서 실행해보기!

```shell
> var x = 0
undefined
> do {
... x++;
... console.log("x: " + x);
... } while(x<3);
x: 1
x: 2
x: 3
undefined
>
```

<br>

<br>

#### Underscore(_) Variable

<br>

> Underscore variable은 최근 결과값을 지칭함!

```shell
$ node
> var x = 10;
undefined
> var y = 5;
undefined
> x + y;
15
> var sum = _
undefined
> console.log(sum)
15
undefined
>
```

<br><br>

### REPL Commands

<br>

- `ctrl + c`

  : terminate the current command

- `ctrl + c` 2번

  : terminate the Node REPL

- `ctrl + d`

  : terminate the Node REPL.

- `위/아래 키`

  : see command history and modify previous commands

- `Tab`

  : list of current commands

- `.help`

  : list of all commands

- `.break`

  : exit from multiline expression

- `.clear`

  : exit from multiline expression

- `.save [filename]`

  : save the current Node REPL session to a file

- `.load [filename]`

  : load file content in current Node REPL session

<br>

<br>

### Stopping REPL

> As mentioned above, use **ctrl + c** twice to come out of Node.js REPL

```shell
$ node
>
(^C again to quit)
>
```

<br>
