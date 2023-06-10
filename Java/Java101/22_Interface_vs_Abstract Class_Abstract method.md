# Interface vs Abstract Class, Abstract method

<br>

### Interface

- `설명`
  - 부모, 자식 관계인 `상속 관계에 얽매이지 않고`, `공통 기능`이 필요할 때 사용한다
    - `Abstract Method` 를 정의해 놓고,
    - `구현 (implements)` 하는 Class 에서 각 기능들을 `Overriding` 하여 여러가지 형태로 구현할 수 있기에 `다형성` 과 연관되어 있다
  - Interface는 해당 Interface를 구현하는 Class 들에 대해 `동일한 method, 동작`을 `강제`하기 위해 존재한다
- `장점`
  - Java 의 `다중 상속`이 안돼서 발생하는 `Abstract Class` 의 한계를 보완해 줄 수 있다
- `단점`
  - 모든 Class가 Interface를 사용한다면, `공통적으로 필요한 기능`도 구현 (implements) 하는 모든 Class에서 Overriding 해 `재정의 해야한다는 번거로움` 이 존재한다
- `정리`
  - Interface는 각각 다른 Abstract Class를 상속하는 Class 들의 `공통 기능을 명시할 때` 사용하면 편리하다

<br>

### Abstract method

- `설명`
  - 자식 class에서 `반드시 overriding` 해야만 하는 method를 의미한다
  - method는 `선언부 ()` 와 `구현부 {}` 로 나누어 지는데, 선언부까지만 작성하고 구현부는 작성하지 않은 method를 의미한다
  - method 내용이 상속받는 class에 따라 달라지기 때문에 추상 method를 사용한다
  - `구현부 {}` 는 해당 class를 상속 받는 하위 class에서 반드시 작성해야 한다
    - 구현부를 작성하지 않으면 `에러`가 발생한다!
  - `주석`으로 어떤 기능을 수행하는 method 인지 설명해야 한다
  - `overriding` method에는 `abstract` 를 작성하지 않는다

<br>

### Abstract Class

- `설명`
  - `Abstract method` 를 하나라도 가지고 있는 class를 `Abstract class` 라고 한다
    - 즉, 일반 class에는 추상 method가 있을 수 없다!
  - Abstract class를 상속 받은 자식 class는 반드시 `abstract method` 를 `overriding` 해야 한다
    - abstract class가 자식 class에게 abstract method의 `재정의를 강요` 한다
    - `abstract class` ↔ `final class`
      - overriding을 제한하기 위해 `상속을 금지` 하는 final class와 반대된다!
  - Abstract class는 `프로그램 설계` 를 목적으로 한다
    - 반면에, 일반 class는 여러 개의 객체를 생성하고, data를 저장하는 것을 목적으로 한다
  - Abstract class는 `객체로 생성할 수 없다`
    - 자식 class에서 abstract class를 상속 받고, abstract method를 `overriding` 하여 구현을 마친뒤, 자식 class를 이요해서 객체를 생성해야 한다
  - 부모와 자식 즉, `상속 관계` 에서 Abstract Class를 `상속 (extends)` 받으며 같은 부모 Class (여기서는 Abstract Class)를 상속받는 `자식 Class들` 간에
    - `공통 기능` 을 각각 `구현`하고,
    - `확장`시키며
    - `상속`과 관련되어 있다
      - 상속은 SuperClass의 기능을 이용, 확장하기 위해 사용된다!
  - Abstract Class를 상속하며 Class들 간의 `구분` 이 가능해 진다
- `장점`
  - Abstract class에서 `설계`가 완료되면, 자식 class에서 상속을 받아 `기능을 확장` 하는데 용이하다
  - 자식 class에서 abstract method의 `구현을 강요` 하기 때문에 `표준화 정도` 를 높인다
  - class 들의 `공통 사항` 을 한 곳에서 관리할 수 있기 때문에 `개발 및 유지보수`가 편리해진다
- `단점`
  - Java에서는 `다중 상속` 을 지원하지 않기 때문에 `Abstract Class` 만으로 구현해야 하는 `Abstract Method`를 `강제`  하는데는 한계가 있다
  - 만약 다중 상속이 가능하다면?

    ```java
    class Vehicle extends Car, Motorcycle {
        @Override
        public void run(){
            super.drive();
        }
    }
    ```

    - Car, Motorcycle에 각각 drive() method가 정의되어 있을 경우, `무엇을 상속받아 Overriding 한 것인지 모호`해 진다
    - 이것이 `다중 상속의 모호성` 이고, 이것 때문에 Java는 다중 상속을 막아 놓았다

<br>

### Abstract Class vs Interface

- Abstract Class는 `IS - A "~이다"` 이고,
  - Interface는 `HAS - A "~을 할 수 있는"` 이다
- Abstract Class는 `상속` 이고,
  - Interface는 `다형성` 이다
