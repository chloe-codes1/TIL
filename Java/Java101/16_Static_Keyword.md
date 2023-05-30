# Static Keyword
>
> static keyword는 field, method, class에 적용할 수 있다
>

<br>

### Static Field (변수, 상수)

- class 안에서 변수를 선언하면 member 변수로 선언이 되고, [`car.name`](http://car.name) 처럼 객체를 통해서 접근해야 한다
- but, static keyword를 사용하여 변수를 선언하면 `Class를 통해서도 접근 가능` 하다
  - Class를 통해서 접근하게 되면, `객체를 만들지 않고` `외부에서 접근`할 수 있다
  - 객체를 통해서도 접근 가능하지만, Class를 통해 접근하는 방법을 권장한다
    - why?
      - member 변수에 접근하는 것인지, static 변수에 접근하는 것인지 쉽게 구분이 안되기 때문!
- static으로 선언된 변수는 `프로그램이 실행될 때` 생성 및 초기화 된다
  - 그렇기 때문에 객체를 생성하지 않아도, `변수는 이미 생성된 상태`이다!
- `final static` 으로 선언하면, 값을 변경할 수 없는 `상수` 가 된다
  - 보통 static 상수를 쉽게 구분하기 위해, 관습적으로 `대문자`와 underscore (`_`) 만을 사용하여 이름을 짓는다
- `접근 제한자`
  - static field를 선언할 때 접근 제한자를 통해 공개하고 싶은 범위를 설정할 수 있다
- `사용하는 이유`
  - 대부분 static field는 `상수를 선언` 할 때 많이 사용한다
    - `final static` keyword로 상수를 선언하면, 다른 Class 에서도 상수에 접근할 수 있다
    - member 변수로 선언할 수도 있지만, 이렇게 구현하면 객체마다 상수들을 갖고 있기 때문에 객체의 크기가 커질 수 있다
  - static으로 변수를 많이 선언하면 객체지향과 거리가 멀어지고, 자칫 스파게티 코드 (복잡하게 얽힌 코드)가 되기 쉬울 수 있다

<br>

### Static Method

- static method도 static field와 유사하다
  - method 선언 시 static keyword를 사용하면, 객체를 생성하지 않아도 해당 method를 호출할 수 있다
- 객체 method를 호출하는 것인지, static method를 호출하는 것인지 구분이 안되기 때문에 `Class를 통해서만 호출` 되어야 한다
- `주의할 점`
  - static method 객체를 생성하지 않아도 호출할 수 있는데, 이것은 `method가 객체와 분리되어 있다` 는 의미이다
    - 그래서 `method 내부`에서 `super` , `this` 와 같은 keyword를 사용할 수 없고,
    - Class의 `member 변수`에 `접근`할 수도 없다
  - static method에서는 method 내부에 선언된 변수 외에 static field, static method만 접근 가능하다
- `사용하는 이유`
  - static method는 보통 `Utils` , `Helper` class를 만드는 데에 사용한다
    - ex) Math라는 Utils class 만들기

      ```java
      public class Math {
          public static double sqrt(double num) {
              // ....
          }
      
          public static double sum(double num1, double num2) {
              // ....
          }
      }
      ```

      - 수학 연산과 관련된 method들을 Math 라는 class 아래로 모아주는 장점이 있다 (`grouping`)

<br>

### Static Class

- static keyword를 이용하여 class를 선언하면, 상위 class와 분리를 해 준다
  - `Inner class` 는 `상위 class와 연결`되어 있기 때문에 상위 class의 member 변수에 접근이 가능하다
    - static으로 하위 class를 선언하면, 상위 class의 member 변수에 접근이 불가능해진다!
    - 이렇게 `static으로 선언된 하위 class` 를 `static nested class` 라고 한다
  - `Static nested class` 는 상위 class가 생성되지 않아도, 외부에서 직접 객체를 생성할 수 있다

    ```java
    Car.Wheel wheel = new Car.Wheel();
    ```

    → 이것이 `Inner class` 와 `Static nested class` 의 가장 큰 차이점이다

- `주의할 점`
  - static class는 `하위 class를 선언할 때`만 가능하다
    - 상위 class를 static으로 선언하려고 하면, compile error가 발생한다
- `static class` 를 사용하는 이유
  - static class로 Inner class를 생성하면 좋은 점은 `grouping`  이다
    - 어떤 class와 연관된 class들을 하위에 선언하여 관련있는 class를 모아둘 수 있는 장점이 있다
      - 이것을 Inner class로도 할 수는 있지만, Inner class는 상위 class와 `연결` 되어 있어 독립된 class가 아니다!

<br>

### Static Keyword 장점 정리

- static keyword의 공통점은 `객체와의 분리` 이다
  - 객체를 생성하지 않고, 접근할 수 있게 해준다!
- `Grouping` 이라는 장점을 갖고 있다
  - 어떤 class 하위에 이와 관련 있는 method, class 를 static으로 선언하여 한 곳에 모을 수 있다!!
