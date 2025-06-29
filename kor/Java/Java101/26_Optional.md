# Optional Class

> java.util.Optional<T> Class
>

<br>

### Optional<T> class 란?

- `Optional<T>` class는 Integer나 Double class 처럼 ‘T’ 타입의 객체를 포함해 주는 `Wrapper class`이다
  - 따라서 Optional 인스턴스는 모든 타입의 참조 변수를 저장할 수 있다
- Optional 객체를 사용하면 예상치 못한 `NullPointerException` 을 간단히 할 수 있다
  - 즉, 복잡한 조건문 없이도 null 값으로 인해 발생하는 예외를 처리할 수 있다

<br>

### Optional 객체의 생성

`of()` method나 `ofNullable()` method를 사용하여 Optional 객체를 생성할 수 있다

- `of() method`
  - null이 아닌 값을 명시하는 값을 가지는 Optional 객체를 반환한다
  - 만약 of() method를 통해 생성된 Optional 객체에 null이 저장되면, `NullPointerException` 예외가 발생한다
- `ofNullable() method`
  - 만약 참조 변수의 값이 null이 될 가능성이 있다면, ofNullable() method를 사용하여 Optional 객체를 생성하는것이 좋다
  - ofNullable() method는
    - 명시된 값이 null이 아니면 명시된 값을 가지는 Optional 객체를 return하고,
    - 명시된 값이 null이면 비어있는 Optional 객체를 반환한다
