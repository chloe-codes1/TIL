# Callbacks Concept in Node.js

<br><br>

### What is Callback?

<br>

- JavaScript에서 함수(function)은 일급 객체임. 
  - 즉, 함수는 **object type**이며 다른 일급 객체와 똑같이 사용될 수 있음
- function 자체가 object이므로 
  - 변수안에 담을 수도 있고,
  - 인수로서 다른 함수에 전달 해 줄수도 있고,
  - 함수에서 만들어질 수도 있고,
  - 반환 될 수도 있음

<br>

#### Callback

: an asynchronous  equivalent for a function

<br>

#### Callback Function

: 특정 함수에 매개변수로서 전달된 함수

  -> *Callback function은 그 함수를 전달받은 함수안에서 호출되게 된다!*

ex)

```javascript
$("#btn_1").click(function() {
    alert("Btn 1 Clicked!")
});
```

- click method의 인수가 변수가 아니라 함수임
  - click method의 인수가 바로 **Callback Function**!

<br>

*Node.js에선 이러한 Callback 함수가 매우 많이 사용된다!*

<br>

<br>

### Blocking Code

- Callback 함수가 사용되지 않는 `Blocking code`
  - 말 그대로 어떤 작업을 실행하고 기다리면서 코드가 *막히게* 됨!

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

- text를 출력하고 program 종료 message 출력됨

<br>

<br>

### Non-Blocking Code

- Callback 함수가 사용된 `Non-Blocking Code`
- 함수가 실행될 때, 프로그램이 함수가 끝날때까지 기다리지 않고 바로 그 아래에 있는 code들을 실행함
  - 그 다음 함수에 있던 작업이 다 끝나면 **callback** 함수를 호출함

<br>

ex)

> input.txt는 blocking code 예시와 같은 file 사용

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

- 모든 Node application의 비동기식 함수에서는 첫번째 parameter로는 **error**를, 마지막 parameter로는 **callback 함수**를 받음
- `fs.readFile()` 함수는 비동기식으로 파일을 읽는 함수
  - 도중에 에러가 발생하면 err 객체에 error 내용을 담고,
  - 그렇지 않을시에는 파일 내용을 다 읽고 출력함!

<br>

> Result

```shell
$ node non-blocking.js 
Program has ended
Let's understand what is a callback function.
What the HELL is it?
```

- `readFile()` method가 실행 된 후, program이 method가 끝날때까지 대기하지 않고 곧바로 다음 명령어로 진행하였기 때문에, program이 끝났다는 message를 출력 한 후에, text 내용을 출력함
  - 그렇다고 program이 끝나고 나서 text 내용을 출력한 것은 아님!
  - program이 실질적으로 끝난건 text가 출력된 후 이다!
    - 만약에 `readFile()` 다음에 실행되는 코드가 그냥 `console.log()`가 아니라 `readFile()` 보다 작업시간이 오래걸리는 코드였다면 text를 먼저 출력하게 될 것!

<br>

<br>

#### Wrap-up

Callback 함수를 사용하여 이렇게 program의 흐름을 끊지 않음으로써, **non-blocking** code를 사용하는 server는 **blocking** code를 사용하는 server 보다 더 많은 양의 요청을 빠르게 처리할 수 있게 된다!

<br>
