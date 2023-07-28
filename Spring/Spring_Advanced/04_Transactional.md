# @Transactional

<br>

### @Transactional 이란?

- @Transactional은 클래스나 메서드에 붙여줄 경우, 해당 범위 내 메서드가 트랜잭션이 되도록 보장해준다
- **선언적 트랜잭션**이라고도 하는데, 직접 객체를 만들 필요 없이 선언만으로도 관리를 용이하게 해주기 때문이다
- 특히나 SpringBoot에서는 선언적 트랜잭션에 필요한 여러 설정이 이미 되어있어 더 쉽게 사용할 수 있다

<br>

### @Transactional(readOnly=true)가 꼭 필요한가?

- 써주는게 좋다!
- why?
  - 조회한 데이터를 return 한다고 해도 `의도치 않게 데이터가 변경되는 일`을 사전에 방지해준다
    - 예상치 못한 Entity의 등록, 변경, 삭제 예방
  - Entity를 `읽기 전용`으로 조회 시, 변경 감지를 위한 snapshot을 유지하지 않아도 되고, 영속성 컨텍스트를 flush 하지 않아도 돼 성능을 최적화 할 수 있다
    - 트랜잭션에 `readOnly=true` 옵션을 주면 스프링 프레임워크가 Hibernate session flush mode를 MANUAL로 설정한다
      - 이렇게 하면 강제로 플러시를 호출하지 않는 한 플러시가 일어나지 않는다!
    - 따라서 트랜잭션을 커밋하더라도 영속성 컨텍스트가 플러시 되지 않아서 엔티티의 등록, 수정, 삭제이 동작하지 않는다
      - 또한 읽기 전용으로 영속성 컨텍스트는 변경 감지를 위한 스냅샷을 보관하지 않으므로 성능이 향상된다
  - 해당 옵션인 경우 CUD 작업이 동작하지 않고, 스냅샷 저장, 변경 감지(dirty check)의 작업을 수행하지 않아 성능이 향상된다
    - `Dirty check` 이란?
      - 상태 변경검사
      - 영속성 컨텍스트와 연결됨
        - JPA에서는 트랜잭션이 끝나는 시점에 변화가 있는 모든 엔티티 객체를 데이터베이스에 자동으로 반영해준다
        - JPA에서는 엔티티를 조회하면 해당 엔티티의 처음 조회 상태 그대로 스냅샷을 만들어 놓는다
        - 그리고 트랜잭션이 끝나는 시점에는 이 스냅샷과 비교해서 다른 점이 있다면 Update Query를 데이터베이스로 전달한다
  - MySQL `이중화 구성(Master - Slave)` 시 DB가 master와 slave로 나누어져 있다면 readOnly = true로 있는 경우에는 읽기 전용으로 master가 아닌 slave를 호출하게 된다
    - 상황에 따라 DB 서버의 부하를 줄이고 약간의 최적화를 할 수 있다
  - @Transactional(readOnly=true) annotation 있다면 코드를 접하는 사람들이 직관적으로 보기에 해당 메서드는 READ에 대한 동작만 수행할 것이라고 예상할 수 있다

<br>

### Spring @Transactional  vs javax @Transactional

- javax @Transactional
  - 자바 표준 확장 패키지
  - 자바에서 기본적으로 제공
- Spring  @Transactional
  - org.springframework에서 제공
  - Spring Container가 관리해준다
- `org.springframework.transaction.annotation.Transactional` 을 사용해야 하는 이유
  - 많은 Option들을 제공한다
    - `isolation`: the underlying database isolation level
    - `noRollbackFor` and `noRollbackForClassName`: the list of Java `Exception` classes that can be triggered without triggering a transaction rollback
    - `rollbackFor` and `rollbackForClassName`: the list of Java `Exception` classes that trigger a transaction rollback when being thrown
    - `propagation`: the transaction propagation type given by the `[Propagation](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/transaction/annotation/Propagation.html)` Enum. For instance, if the transaction context can be inherited (e.g., `REQUIRED`) or a new transaction context should be created (e.g., `REQUIRES_NEW`) or if an exception should be thrown if no transaction context is present (e.g., `MANDATORY`) or if an exception should be thrown if a current transaction context is found (e.g., `NOT_SUPPORTED`).
    - `readOnly`: whether the current transaction should only read data without applying any changes.
    - `timeout`: how many seconds should the transaction context be allowed to run until a timeout exception is thrown.
    - `value` or `transactionManager`: the name of the Spring `TransactionManager` bean to be used when binding the transaction context.
