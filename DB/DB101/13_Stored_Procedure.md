# Stored Procedure

<br>

## Stored Procedure 란?

- 일련의 쿼리를 마치 `하나의 함수`처럼 실행하기 위한 `쿼리의 집합`
  - `여러개의 쿼리`를 하나의 함수로 `묶은 것`

<br>

## Stored Procedure 의 장점

- 재사용성 및 중복 코드 최소화
  - 같은 작업을 수행하는 SQL문을 반복해서 작성하지 않고 재사용 할 수 있다
  - SQL에 IF나 While과 같은 제어 문장을 사용할 수 있어서 애플리케이션 소스 코드를 줄일 수 있다
- 네트워크 부하 감소
  - Stored Procedure는 DB 내에서 실행되기 때문에 client ↔ db server 간의 네트워크 트래픽을 감소시킬 수 있다
  - 복잡한 쿼리나 데이터 처리를 client에서 요청하는 것이 아니라 sever에서 수행되기 때문에 성능을 향상시킬 수 있다
- `처리 시간` 감소 및 성능 향상
  - 일련의 SQL문을 한 번에 실행할 수 있기 때문에 개별적으로 실행하는 것보다 성능이 향상된다
  - DB server가 stored procedure를 미리 컴파일하고 최적화하여 실행 계획을 생성하기 때문에 보다 빠른 실행 속도와 성능을 제공한다
- 데이터 `무결성` 유지
  - Stored Procedure 내에서 복잡한 데이터 검증 로직등을 처리하여 무결성을 유지할 수 있다
  - Stored Procedure 내에서 여러 작업을 하나의 트랜잭션으로 묶어 여러 테이블 간의 일관성을 보장하거나, 실패한 경우 롤백하여 데이터 일관성을 유지할 수 있다

<br>

## Stored Procedure 의 단점

- 복잡성 증가
  - 코드가 DB 내부에 저장되므로 application에서 관리하는 것 보다 디버깅, 테스트, 그리고 유지보수가 어려울 수 있다
- 불편한 유지보수
  - DB 내부에 저장되기 때문에 SCM을 활용한 버전 관리, 변경을 추적하거나 롤백하는 작업이 어렵다
- DB 확장 어려움
  - Stored Procedure의 문법과 기능은 DB 벤더마다 다를 수 있어서 특정 벤더에 종속되게 만들 수 있다
    - 이로 인해 DB를 변경하거나 이관할 때 수정이 필요할 수 있다
- 성능 최적화의 제한
  - DB engine 내에서 독립적으로 실행되기 때문에 application level에 작성된 코드보다 최적화하기 어려울 수 있다
    - 이로 인해 복잡한 쿼리 최적화를 위해서는 DB engine 내부 동작을 이해해야할 필요가 있다
- 테스트의 어려움
  - 테스트가 DB 내부에서 이루어지므로 application level에서 테스트를 하는 것보다 복잡하고 번거로울 수 있다
