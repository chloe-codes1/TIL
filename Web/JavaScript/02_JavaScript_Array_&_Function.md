# JavaScript Arrays and Functions

<br><br>

## JavaScript Arrays

<br>

### Array

> JavaScript에서 배열은 값만 존재한다

<br>

- 배열 리터럴

  ```javascript
  var a = [1,2,3]
  ```

  <br>

- Array 생성자 함수

  ```javascript
  var b = new Array(1,2,3)
  ```

  <br>

  <br>

### Array 순회

- `for`

  ```javascript
  var a = [1,2,3]
  
  for (var i=0 ; i <a.length; i++){
      console.log(i, a[i])
  }
  ```

  <br>

- `for .. of`

  : 안에 있는 원소 값들을 하나 하나씩 출력

  ```javascript
  for (var elem of a){
      console.log(elem)
  }
  ```

  <br>

- `forEach`
  
  : 인자로 함수 자체를 받음
  
  ```javascript
  a.forEach( function(elem, idx) {
      console.log(idx, elem)
  })
  ```
  
  <br>
  
- `for .. in`

  - 배열 요소만 접근하는 것이 아니라 속성까지 출력될 수 있다
    - JavaScript에서 배열도 object라서 속성 설정이 가능하지만, 리스트의 속성이 아니라, Object의 속성이 된다

  ```javascript
  var a = [1,2,3]
  
  a.name = 'myarr'
  
  for (var i in a){
      console.log(i, a[i])
  }
  
  //0 1
  //1 2
  //2 3
  //name myarr   => 속성까지 순회
  ```

  - *for ... in 형태는 사용 시 주의해야함!*
    - for ...in 은 Object 자체의 모든 속성을 순회한다

<br>

<br>

### Array methods

<br>

- `sort`
  - 비교 함수가 (인자) 없으면 **문자열을 기준으로** 정렬한다
    - 이게 싫다면 비교 함수를 인자로 넣기
  - 비교함수가 있다면, 해당 함수의 return 값이 0보다 작음으로 정렬한다

<br>

- 문자열 관련
  - `join`
    - 배열.**join**('haha')
- `toString`
  
- 배열 합치기
  
  - `concat`
  
    : 두 개의 배열을 합쳐줌
  
- 원소 삽입/삭제

  - `push`
  - `pop`
  - `unshift`
    - 왼쪽 끝에 넣기
  - `shift`
    - 왼쪽 끝에 있는 것 빼기

- index 탐색

  - `indexOf`

- 배열 조작

  - `splice(start[, deleteCount[, item1[, item2[, ...]]]])`

    - 원본 배열 자체를 바꿔버림

    - 원소의 수정/삭제도 가능

      ```javascript
      var a = [1,2,3]
      a.splice(1,2, "처음", "두번") // 1번째 위치부터 두 개를 지우겠다 + "처음", "두번" 을 붙이겠다
      // [1, "처음", "두번"]
      
      var a = [1,2,3]
      a.splice(1,2, "처음") //1번째 위치부터 두 개를 지우겠다 + "처음" 을 붙이겠다
      // [1, "처음"]
      ```

- 배열 자르기

  - `slice`

    : return을 해줌

<br>

<br>

## JavaScript Functions

<br>

### 함수 선언

<br>

#### 1. 함수 선언문

```javascript
function sum(a,b) {
    return a+b;
}
sum(1,2) //3
```

<br>

#### 2. 함수 표현식

```javascript
// 변수에 익명함수를 할당
var sub = function(a,b) {
    return a - b;
}
sub(1,2) //-1
```

<br>

#### 3. 즉시 실행 함수

```javascript
(function(a,b){return a*b})(1,2) //2
```

<br>

#### 4. 화살표 함수 (ES6)

```javascript
var sum = (a,b) => a+b  //a+b 한 줄이라서 중괄호{} 생략함
sum(3,4) //7

var area = (r) => {
    const PI = 3.14;
    return r*r*PI;
}
area(1) //3.14
```

<br>

<br>

### 함수 인자

- JavaScript에서 함수는 매개변수 전달에 대한 제한이 없음

- `arguments` 객체는 매개변수로 넘겨진 모든 정보를 가지고 있음

  ```javascript
  function foo(a) {
      console.log(arguments); //arguments 찍어서 확인 해보기
      return a
  }
  ```

  - 어떤 인자도 넣어주지 않으면 undefined 라고 뜸

    - `undefined`

      : JavaScript에서 변수를 초기화 할 때 할당 해 놓는 값

<br>

<br>
