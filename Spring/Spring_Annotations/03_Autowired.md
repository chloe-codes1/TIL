# @Autowired

<br>

### Autowired 란?

- Spring Framework에서 사용되는 annotation으로, `자동 주입`을 위해 사용된다
- Spring은 DI (Dependency Injection)을 통해 객체들 간의 관계를 설정하고, 이를 통해 application의 loose coupling을 유지한다
  - 이를 위해 **`@Autowired`** annotation을 사용하여 Spring Container가 해당 field, constructor 또는 method parameter에 해당하는 Bean 객체를 자동으로 주입하도록 지정할 수 있다
- @Autowired annotation을 사용하면 의존 객체를 직접 생성하거나 주입하지 않고도 Spring Framework가 자동으로 주입해주기 때문에, 코드의 복잡성을 줄이고 유지보수를 쉽게 할 수 있다

<br>

### @Autowired 적용 시 의존 객체를 찾는 순서

1. 타입이 같은 bean 객체를 검색한다
    - 1개이면 해당 bean 객체를 사용한다
    - @Qualifier가 명시되어 있는 경우, 같은 값을 갖는 bean 객체여야 한다
2. 타입이 같은 bean 객체가 두개 이상이고, @Qualifier가 없는 경우 `이름이 같은` 빈 객체를 찾는다

    → 찾은 경우 그 객체를 사용

3. 타입이 같은 bean 객체가 두개 이상이면, @Qualifier로 지정한 bean 객체를 찾는다

    → 찾은 경우 그 객체를 사용

4. 위 경우 모두 해당되지 않으면 컨테이너가 Exception을 발생시킨다
