# Lombok

## Lombok 이란?

개발할 때 자주 사용하는 코드 Getter, Setter, 기본 생성자, toString 등을 annotation 으로 자동 생성해준다

## Lombok Annotations

### @Getter

Class내에 선언된 모든 field의 get method를 생성해 준다

### @RequiredArgsConstructor

- 선언된 모든 `final` field 를 인자값으로 하는 생성자를 생성해 준다
  - final 이 없는 field는 생성자에 포함되지 않는다
- 사용하는 이유
  - 해당 class의 의존성 관계가 변경될 때마다, 생성자 코드를 계속해서 수정하는 번거로움을 해결하기 위함

### @NoArgsConstructor

- 기본 생성자를 생성해 준다
- `public Post() {}` 와 같은 효과

### @Builder

- 해당 Class의 Builder pattern class를 생성한다
- Class 상단에 선언 시 생성자에 포함된 field만 builder에 포함
- Options
  - `toBuilder`
    - default = false
    - true로 설정 시 builder로 만든 인스턴스에서 `toBuilder()` method를 호출해 그 인스턴스 값을 베이스로 Builder Pattern으로 새로운 인스턴스를 생성할 수 있다
