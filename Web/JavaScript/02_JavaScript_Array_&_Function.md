# JavaScript Arrays and Functions

<br><br>

## JavaScript Arrays

<br>

### Array 순회

- `for`
- `for .. of`
  - 안에있는 원소 값들을 하나하나씩 출력
- `forEach`
  - 인자로 함수 자체를 받음

- `for .. in`
  - 배열 요소만 접근하는 것이 아니라 속성까지 출력될 수 있다
    - JavaScript에서 배열도 object라서 속성 설정이 가능하지만, 리스트의 속성이 아니라 ....

<br>

<br>

### Array method

<br>

- sort
  - 비교 함수가 (인자) 없으면 문자열을 기준으로 정렬한다
  - 비교함수가 있다면, 해당 함수의 return 값이 0보다 작음으로 정렬한다

<br>

- 문자열 관련 
  - `join` 
  - `toString`

- 배열 합치기 
  -  `concat`

- 원소 삽입/삭제

  - push
  - pop
  - unshift
  - shift

- index 탐색

  - indexOf

- 배열 조작

  - splice

    : 원본 배열 자체를 바꿔버림

- 배열 자르기

  - slice

    : return을해줌



<br>

<br>

## JavaScript Functions

<br>

### 함수 선언

<br>

#### 1. 함수 선언문

<br>

#### 2. 함수 표현식

<br>

#### 3. 즉시 실행 함수

<br><br>

#### 4. 화살표 함수 (ES6)

<br>

<br>

### 함수 인자

- JavaScript에서 함수는 매개변수 전달에 대한 제한이 없음
- arguments 객체는 매개변수로 넘겨진 모든 정보를 가지고 있음