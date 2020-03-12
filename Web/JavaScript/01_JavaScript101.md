# JavaScript Basics

<br>

<br>

### JavaScript의 기능

- HTML & CSS
  - Web 문서의 구조와 외형을 정의
- JavaScript
  - 문서의 **기능**을 정의

<br>

#### ES2015 (ES6)

- JavaScript의 고질적인 문제들을 많이 해결한 ES2015를 지나 현재 ES2019까지 발표

<br>

#### Vanilla JS (순수한 JavaScript)

- Cross browsing, 간편한 활용 등을 위해 많은 library들이 등장 (대표적으로 jQuery)
- 최근 표준화된 browser, ES6 이후의 다양한 도구의 등장으로 순수 JavaScript 활용의 증대

<br>

#### Browser에서 할 수 있는 일

- 전역 객체 window
  - DOM 조작
  - BOM 조작

<br>

*V8 engine을 기반으로 한 Node.js*



<br>

### JavaScript의 특징

<br>

1. #### Script 언어이다

   - Interpreter를 통해 바로 실행된다
   - Data type, type casting 수월
   - 속도가 느림
   - 실행 환경에 제한을 받음
     - JavaScript Interpreter 가 설치되어있는 프로그램에서만 작동함

<br>

2. #### 함수형 언어이다

   - 함수를 기본으로 하는 방식
   - 선언적 프로그래밍
     - HTML 요소를 동적으로 처리 가능
   - 1급 함수
     - 함수 자체를 data 처럼 사용 가능
   - 변수의 유효 범위 == 함수의 유효 범위

<br>

3. Java와는 전혀 다른 programming 언어이다
   - Netscape 사에서 마케팅을 목적으로 Java 라이센스를 받아 사용
   - JavaScript == ECMA-262

<br>

4. 초보적인 언어가 아니다
   - 학습 시작 초기에는 쉽지만 복잡한 서비스 구축에 사용될만큼 강력함

5. Web 표준이다
   - HTML5: HTML5 + CSS3 + JavaScript
   - HTML5의 JavaScript에 대한 의존도가 높음

<br>

*JavaScript는 함수형 프로그래밍에 적합하다!!!*



<br>

#### Pros of JavaScript

1. Text editor와 web browser만 있으면 programming 가능
2. Data type 및 type-casting이 쉬워 쉽게 학습하여 사용 가능
3. Compile 과정을 거치지 않기 때문에 작성한 코드 테스트가 수월

<br>

<br>

## Data Types & Variables

<br>

### JavaScript 구문

<br>

#### JavaScript 기본 구문

- 해석 순서

  - Interpreter에 의해 위에서 아래로 해석 & 실행됨

    - `Interpreter`

      : 프로그램 언어로 적혀진 프로그램을 기계어로 변환하는 프로그램

- 대/소문자 구분

  - variable, method, keyword

- 구문 끝

-  공백과 들여쓰기

- 주석



<br>

<br>

### Data Type 분류 (typeof)

<br>

#### 1. 원시 타입 (primitive) 

> 변경 불가능한 값 (immutable)



<br>

#### 2. 객체 타입 (object)

- object: 일반 객체, function, array

<br>

<br>

### Data Type

<br>

#### Number

- Integer Type이 별도로 없는 것이지 정수라는 수 체계가 존재하지 않는 것은 아니다

<br>

#### String 

- Template 문자열

<br>

#### null vs undefined

- undefined
  - 
- null
  - 선언 했는데 값이 할당되지 않은 경우
  - typeof null => object 라고 나옴

<br>

#### Object

- JavaScript는 원시 타입 (primitive type)을 제외하고는 모두 객체이다
- JavaScript의 객체는 key와 value로 구성된 속성 (property)의 집합이다
- 값 == 함수?
  - method로 불리움

<br>

#### 변수 유효 범위 (scope)

- 함수 level scope를 가진다
- 함수 내에서 선언된 변수는 지역변수이며, 나머지는 전역변수로 활용
- 변수 선언 시 키워드(var)를 쓰지 않으면, 암묵적 전역으로 설정된다
  - 주의: 변수가 아닌 전역 객체 (window)의 property로 생성 
    - 변수에 할당된 것이 아니라 window.global 이 된 것!
  - keyword를 꼭 사용해라!

<br>

#### 호이스팅과 let, const(ES6)

- JavaScript에서는 모든 선언을 호이스팅 한다
- ES6에서 새롭게 등장한 let과 const keyword는 이러한 내용을 방지할 수 있다
  - 호이스팅 자체가 이루어 지는 것은 아니고, var는 선언과 동시에 초기화 (undefined)를 하고, 
  - let, const는 선언과 초기화 단계가 분리되어 진행된다
- Block level scope를 가지고 있다

<br>

<br>

### JavaScript 문법

<br>

#### `==` vs `===`

- 동등 연산자 (==)
- 일치 연산자 (===)

<br>

#### 조건문

- else if
- {}

<br>

#### 반복문

- {}

<br>

<br>

