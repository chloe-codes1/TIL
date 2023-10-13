# @Immutable

> Reference: [@Immutable in Hibernate](https://www.baeldung.com/hibernate-immutable)
>

### @Immutable 이란?

- 해당 annotation을 `Entity` 에 추가하면, update가 작동하지 않는다
- `Collection` 에 추가하면, add & delete 작동하지 않는다

### @Immutable annotation을 추가했을 때 달라지는 동작

- INSERT
  - 달라진 점이 없다
- UPDATE
  - Hibernate는 exception을 일으키지 않고 그냥 UPDATE 작업 실행을 `무시`한다
  - exception이 발생하게 하려면, 따로 설정이 필요하다
- DELETE
  - 달라진 점이 없다

### 주의할 점

- `@Immutable` 엔티티는 여전히 JPQL이나 Criteria로 업데이트 가능하다
- but, **5.2.17**부터는 업데이트를 막았으나 WARNING만 남긴다
  - 여기에 오류까지 발생시키려면 아래 property를 설정하면 된다

    ```java
    hibernate.query.immutable_entity_update_query_handling_mode=exception
    ```
