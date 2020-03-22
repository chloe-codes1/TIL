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

- Callback 함수가 사용되지 않는 Blocking code
  - 말 그대로 어떤 작업을 실행하고 기다리면서 코드가 *막히게* 됨!

<br>

ex)

> input.txt file

```
Let's understand what is a callback function.
What the HELL is it?
```

<br>

> main.js

```javascript
var fs = require("fs");

var data = fs.readFileSync('input.txt')

console.log(data.toString());
console.log("Program has ended!")
```

<br>

> Result

```shell
$ node main.js
Let's understand what is a callback function.
What the HELL is it?
Program has ended!
```

- text를 출력하고 program 종료 message 출력됨

<br>

<br>





