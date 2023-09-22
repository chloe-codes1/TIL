# JavaScript Object

<br>

<br>

#### Terms

- `생성자 함수`

  : new 연산자를 통해 객체를 생성하고 property와 method를 생성하여 초기화하는 JavaScript 함수
  
- `Prototype`

  - 생성자 함수의 property
  - 생성자 함수로 생성된 객체들이 동일하게 상속받는 property와 method가 정의되는 곳

- `비공개 member`

  : 객체 외부에서는 수정할 수 없는 property or method

<br>

<br>

### JavaScript Object

- Primitive data type을 제외한 모든 data type은 Object

  - `Primitive Types`

    - **number**

    - **string**

    - **boolean**

    - **null**

      : no value

    - **undefined**

      : a declared variable, but hasn't been given a value

    - **symbol**

      : a unique value that's not equal to any other value

- 함수도 객체다

<br>

<br>

### 객체의 생성

<br>

#### 객체

: property 의 모음

<br>

#### 객체의 생성

- 객체 literal 의 경우 객체 property 를 나열하여 생성

- 빈 객체

  : literal 방식의 함수 생성 시 property를 쉽게 추가할 수 있어어 사용

- `namespace`

  : 변수와 함수 등의 객체의 property로 변경하여 전역변수 사용 최소화

- new 연산자와 생성자 함수를 사용하여 객체를 생성함

<br>

#### 생성자 함수와 prototype

- `this`

  : method 에서 사용되며 method를 호출한 호출 객체를 가리킴

- `생성자 함수`

  - 생성할 객체에 어떤 property가 있을 것이며 그 property는 어떻게 초기화 될 것인지를 정의해 놓은 함수
  - 일반적인 객체지향 언어의 class와 유사

- `prototype`

  - 객체 dml property를 생성된 객체에 복사해 오는 것이 아니라 참조하고 있다는 것을 의미
  - 생성자 함수의 prototype 객체가 수정되면 이 생성자 함수에 의해 생성된 객체의 property가 변경 되는것!

  <br>
