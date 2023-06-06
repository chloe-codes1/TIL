# Access Modifiers

<br>

<br>

### 접근 제한자 (Access Modifier)

<br>

#### Public

: 모든 접근을 허용

#### Protected

: 같은 패키지 (폴더)에 있는 객체와 상속 관계의 객체들만 허용

#### Default

: 같은 패키지 (폴더) 내에 있는 객체들만 허용   => same package

#### Private

: 현재 객체 내에서만 허용   => same class

<br><br>

### 접근 제한법

- 접근 제한법을 이용하여 자료(instance 변수)를 외부로부터 직접적인 접근을 차단하고, 자료를 수정 또는 동작할 수 있는 동작들은 내부에 둔다.
  - 이렇게 하면 외부에서는 내부에서 어떤 변화가 있는지 알 수 없고, method를 통해 결과만 받을 수 있음

    => 정보 은닉이 가능하다

  <br>

![img](https://lh4.googleusercontent.com/YtBtKe9qZKtVHKwHfBag3a5UgEdOXqXK1o7USx3p3-F59NIYFUZ1lF0Ph5EhY1POdQDsR6wD5p1y3lRi5JJvxzUsfbjsXwnYwAo8--yfw3s5ErluAz98YqvDisESvdeAKsBByZQ8)

<br><br>

`+`

#### Getters Setters method

: two conventional methods that are used for retrieving and up-dating value of a variable.

- Eclipse 맨 위 메뉴 source - Generate Getters Setters method 사용

- boolean type만 set___이 아니라 is___ 임!
