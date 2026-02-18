# Callbacks Concept in Node.js

<br><br>

### What is Callback?

<br>

- In JavaScript, functions are first-class objects.
  - That is, functions are of the **object type** and can be used just like other first-class objects
- Since a function itself is an object,
  - it can be stored in a variable,
  - passed as an argument to another function,
  - created within a function,
  - and returned from a function

<br>

#### Callback

: an asynchronous  equivalent for a function

<br>

#### Callback Function

: A function passed as a parameter to a specific function

  -> *The callback function is called within the function that received it!*

ex)

```javascript
$("#btn_1").click(function() {
    alert("Btn 1 Clicked!")
});
```

- The argument of the click method is a function, not a variable
  - The argument of the click method is the **Callback Function**!

<br>

*Such Callback functions are used very frequently in Node.js!*

<br>

<br>

### Blocking Code

- `Blocking code` where Callback functions are not used
  - As the name suggests, the code is *blocked* while executing and waiting for a task!

<br>

ex)

> input.txt file

```
Let's understand what is a callback function.
What the HELL is it?
```

<br>

> blocking.js

```javascript
var fs = require("fs");

var data = fs.readFileSync('input.txt')

console.log(data.toString());
console.log("Program has ended!")
```

<br>

> Result

```shell
$ node blocking.js
Let's understand what is a callback function.
What the HELL is it?
Program has ended!
```

- The text is printed first, then the program end message is printed

<br>

<br>

### Non-Blocking Code

- `Non-Blocking Code` where Callback functions are used
- When a function is executed, the program does not wait for the function to finish and immediately executes the code below it
  - Then when the task in the function is done, the **callback** function is called

<br>

ex)

> The same input.txt file from the blocking code example is used

<br>

> non-blocking.js

```javascript
var fs = require("fs");

fs.readFile('input.txt', function (err, data) {
    if (err) return console.error(err);
    console.log(data.toString());
});

console.log("Program has ended");
```

- In all asynchronous functions of Node applications, the first parameter receives an **error** and the last parameter receives a **callback function**
- The `fs.readFile()` function reads a file asynchronously
  - If an error occurs during the process, the error content is stored in the err object,
  - Otherwise, it reads all the file content and prints it!

<br>

> Result

```shell
$ node non-blocking.js
Program has ended
Let's understand what is a callback function.
What the HELL is it?
```

- After the `readFile()` method was executed, the program did not wait for the method to finish and proceeded directly to the next command, so the program end message was printed before the text content
  - However, this does not mean the text content was printed after the program actually ended!
  - The program actually ended after the text was printed!
    - If the code executed after `readFile()` was not just a simple `console.log()` but code that takes longer than `readFile()`, the text would have been printed first!

<br>

<br>

#### Wrap-up

By using Callback functions to avoid interrupting the program flow like this, a server using **non-blocking** code can handle a larger volume of requests faster than a server using **blocking** code!

<br>
