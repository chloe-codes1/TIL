# JavaScript Functions

<br>

<br>

### 익명 함수

> 이름 없이 생성되는 함수

- 생성되어 변수에 할당
  - 변수는 함수의 이름 역할을 함!
- 선언적 함수 정의를 통해 생성된 함수의 이름도 함수를 가리키는 변수이다!

<br><br>

### 함수 호이스팅

- JavaScript 에서는 모든 선언이 호이스팅 된다
- 함수 선언문의 경우 선언, 초기화, 할딩이 모두 이뤄져 실행 가능
- 함수 표현식은 변수 호이스팅이 발생하여 undefined. 즉, 실행 불가

<br>

<br>

### 배열 테스트 함수 (Call-back 함수)

> Call-back 함수: method 실행 시 자동으로 호출되는 함수

<br>

#### Array helper methods

> 배열 검사 method의 call-back 함수

<br>

- `forEach`

  - Element 하나하나 조작 시 사용

  - Element 하나하나 call-back 함수에 전달하여 처리

  - Usage

    ```javascript
    arr.forEach( callback(currentvalue[, index[, array]] [, thisArg]))
    ```

    ```javascript
    function hiUser(element, index, array){
        document.write("<p>Hi " +element+ "!</p>")
    }
    var users = ["jerry", "tom", "steve"];
    users.forEach(hiUser);
    ```

    <br>

- `map`

  - 배열 요소 하나 하나에 call-back 함수 처리 후 새로운 배열 반환

    ```javascript
    function sayBabyAnmial(animal){
        var result;
        switch(animal){
            case "개":
                result = "강아지";
            break;
            case "닭":
                result = "병아리";
            break;
            default:
                result = "새끼 " + animal;
        }
        return result;
    }
    var animals = ["고양이", "개", "다람쥐", "닭","여우"];
    var baby = animasl.map(sayBabyAnimal);
    ```

    <br>

- `filter`

  - 원하는 요소를 정리하여 새로운 배열 반환

    - 요소 정리할 때 call-back 함수 사용

  - 배열 객체 검사용 method 사용시 call-back 함수 전달 인자

    1. element
    2. index
    3. array

    ```javascript
    function isBigEnough(element, index, array){
        return (element >= 10);
    }
    var filtered = [12, 5, 8, 130, 44].filter(isBigEnough);
    document.write(filtered.toString()); //12,130,44
    ```

    <br>

- `every`

  - 모든 배열 요소 call-back 함수에서 제시하는 요소 통과 시 return  **true**, 실패 시 return **false**

    ```javascript
    function isBigEnough(element, index, array){
        return (element >= 10);
    }
    var passed = [12, 5, 8, 130, 44].every(isBigEnough); //false
    var passed = [12, 54, 18, 130, 44].every(isBigEnough); //true
    ```

    <br>

- `some`

  - every와 논리적으로 반대되는 경우
    - call-back 함수 요구하는 element 한 개라도 존재: return **true**
    - 하나도 없으면: return **false**

<br>

<br>

### 함수의 유효 범위

<br>

- JavaScript === 함수형 언어

- 함수를 기준으로 유효 범위 설정

  - **함수**

    : 자신만의 유효 범위 설정

    - 함수 내부에서 선언된 변수 => 함수 내부에서만 유효

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

- 밖에 있었던 변수 등을 안에서도 기억하고 있는 것!!!

<br>

<br>

#### LEGB rule

- local
- environment
- global
- build-in

![LEGB figure](https://sebastianraschka.com/images/blog/2014/scope_resolution_legb_rule/scope_resolution_1.png)
