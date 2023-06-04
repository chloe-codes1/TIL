# Overriding vs Overloading

<br>

## 오버로딩 (Overloading)

### 오버로딩이란?

하나의 class에 사용하려는 이름과 같은 이름을 가진 method가 있더라도 `parameter의 개수 또는 타입`이 다르면,

같은 이름을 사용해서 method를 정의할 수 있는 것 → 새로운 method를 정의

<br>

### 오버로딩의 조건

- Method `이름이 같고`, `parameter`의 `개수`나 `타입`이 달라야 한다
- return 값만 다른 것은 오버로딩 할 수 없다!

<br>

### 오버로딩을 사용하는 이유

- 같은 기능을 하는 method를 하나의 이름으로 사용할 수 있다
  - ex) println
    - 인자 값으로 int, double, boolean, String 등 다양한 타입의 매개 변수를 집어 넣어도, 우리는 그 함수들이 어떻게 실행되는지는 모르지만 console 창에 출력을 해주는 것을 볼 수 있다
- method 이름을 절약할 수 있다

<br>

## 오버라이딩 (Overriding)

### 오버라이딩이란?

- 부모 class로부터 상속받은 method를 자식 class에서 `재정의` 하는 것
- 상속받은 method를 그대로 사용할 수 있겠지만, 자식 class에서 상황에 맞게 변경해야 하는 경우 오버라이딩을 할 필요가 생긴다

<br>

### 오버라이딩의 조건

- 오버라이딩이란 method의 동작만을 재정의하는 것이므로, method의 `선언부는 기존 method와 완전히 같아야` 한다 (method 이름, parameter)
  - but, method의 return type은 부모 class의 return type으로 type 변환할 수 있는 type이라면 변경할 수 있다
- 부모 class의 method 보다 `접근 제어자` 를 더 `좁은 범위` 로 변경할 수 없다
- 부모 class의 method 보다 더 `큰 범위`의 `예외`  를 선언할 수 없다

<br>

### @Override의 용도

- @Override 어노테이션은 오버라이딩을 `검증하는 기능`을 한다
- 오버라이딩이 실제로 시행되지 않았다면, `컴파일 시 오류`를 출력한다
