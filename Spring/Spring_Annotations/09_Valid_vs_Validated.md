# @Valid vs @Validated

> Reference:[Baeldung - Differences in @Valid and @Validated Annotations in Spring](https://www.baeldung.com/spring-valid-vs-validated)

## @Valid and @Validated

`@Valid`를 적용할 때는 제약조건을 설정한 속성에 대해 `전부 유효성 검사`를 하게 되는데,
만약 제약조건은 그대로 선언하되 **`원하는 속성만 유효성 검사를 하고 싶은 경우`**에 `@Validated` 를 사용할 수 있다

## @Valid vs  @Validated

### Target

> `@Validated` 는 `@Valid` 의 기능을 포함한다
>
>
> →  `@Valid` 를 적용한 곳이라면 `@Validated` 로 변경 가능하다
>
- `@Valid`
  - parameter나 method 내 객체의 유효성 검사를 수행하는 데 사용된다
  - class 수준 유효성 검사에는 사용되지 않는다
- `@Validated`
  - method 수준의 유효성 검사와  class 수준 유효성 검사를 모두 지원한다

### Group Validation Support

- `@Valid`
  - Group 유효성 검사를 지원하지 않는다
- `@Validated`
  - 검토할 검토 option의 group을 지정할 수 있다
  - group을 지정하여 특정 group에 대한 유효성 검사를 적용하거나 생략할 때 사용할 수 있다

### Validation Method

- `@Valid`
  - **javax.validation.Validator**
- `@Validated`
  - **org.springframework.validation.Validator**
    - Spring의 유효성 검사 방법과 통합되어 있다
    - `@Validated` annotation을 사용하면 Spring은 Validator 구현체를 활용하여 해당 객체의 유효성 검사를 수행한다

### Exception Handling

- `@Valid`
  - **javax.validation.ConstraintViolationException** 이 발생한다
- `@Validated`
  - Spring의 **MethodArgumentNotValidException** or **BindException**이 발생할 수 있으며, 이러한 예외를 처리하기 위한 custom message나 handler를 구성할 수 있다
