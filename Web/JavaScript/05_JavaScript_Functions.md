# JavaScript Functions

<br>

<br>

### 함수 호이스팅

- JavaScript 에서는 모든 선언이 호이스팅 된다
- 함수 선언문의 경우 선언, 초기화, 할딩이 모두 이뤄져 실행 가능
- 함수 표현식은 변수 호이스팅이 발생하여 undefined. 즉, 실행 불가

<br>

#### Array helper methods

구문

```javascript
arr.forEach( callback(currentvalue[, index[, array]] [, thisArg]))
```

- map
- filter

<br><br>

### Closure

<br>

#### First class function

- JavaScript 함수의 특징
  - 함수를 인자로 전달 가능함
  - 함수를 반환할 수 있음
  - 변수에 함수를 할당 가능함
- 위의 조건은 programming 언어에서의 일급객체 (first class object / first class citizen) 의 조건이다
- 함수를 인자로 전달
- 함수를 반환

<br>

#### Closure

: closure는 함수와 함수가 선언된 어휘적 환경 (lexical scoping, environment)의 조합이다

```javascript
function makeAdder() {
    var x =1
    return function(y){
        return x+y
    }''
}
var add1 = 
```





#### LEGB rule

- local
- environment
- global
- build-in

