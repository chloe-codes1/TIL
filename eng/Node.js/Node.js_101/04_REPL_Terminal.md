# REPL Terminal

<br>

<br>

### REPL (Read Eval Print Loop)

> Refers to an environment where the system returns a value when the user enters a command, similar to the Windows command prompt or UNIX/LINUX Shell

<br>

Node.js comes with a REPL environment and can perform the following functions

- **Read**

  : Reads the user's input, converts it into JavaScript data structures, and stores it in memory

- **Eval**

  : Evaluates (processes) the data

- **Print**

  : Prints the result

- **Loop**

  : Repeats Read, Eval, Print until the user presses `ctrl + c` twice to exit

<br>

*Node.js's REPL environment is useful for testing & debugging JavaScript code!*

<br>

<br>

### Starting REPL

<br>

> REPL can be started by running node without any parameters in the Shell / Console

```bash
$ node
>
```

<br>

#### 1. Using simple expressions

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

#### 2. Using variables

- Like other scripts, you can store values in variables and print them later
- When using the `var` keyword
- The value of the variable is not printed when the command is entered,
- When the `var` keyword is not used
  - The value of the variable is printed
- You can print using **console.log()**

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

#### 3. Using Multi-line Expressions

<br>

> Run a do-while loop in REPL!

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

> The underscore variable refers to the most recent result!

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

- `ctrl + c` twice

  : terminate the Node REPL

- `ctrl + d`

  : terminate the Node REPL.

- `Up/Down keys`

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
