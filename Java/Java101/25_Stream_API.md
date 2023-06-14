# Stream API

<br>

### Steam API란?

- 데이터를 추상화하여 다뤄서, 다양한 방식으로 저장된 데이터를 읽고 쓰기위한 공통된 방법을 제공한다
  - Steam API를 이용하면, 배열이나 Collection 뿐만 아니라 파일에 저장된 데이터도 모두 같은 방법으로 다룰 수 있다
- 배열, 리스트 등 컬렉션의 저장 요소를 하나씩 참조해서 람다식으로 처리할 수 있도록 해주는 기능이다
- Collection 내부의 데이터 정렬, 필터링, 중복 제거 등을 구현 시 필요하다

<br>

### Stream의 특징

- Stream은 외부 반복을 통해 작업하는 컬렉션과 달리, `내부 반복 (internal iteration)` 을 통해 작업을 수행한다
- Stream은 `일회용`이다
  - Stream은 재사용이 가능한 Collection과는 달리, 한 번 사용하면 닫혀서 재사용이 불가능하다
  - 필요하다면 정렬된 결과를 Collection이나 배열에 담아서 return 할 수 있다
- Stream은 `원본 데이터를 변경하지 않는다`
  - Stream은 원본 데이터로부터 데이터를 읽기만 할 뿐, 원본데이터 자체를 변경하지 않는다
- Stream 연산은 `필터-맵 (filter-map)` 기반의 API를 사용하여 `지연 (lazy) 연산`을 통해 성능을 최적화한다
- Stream은 `parallelStream()` method를 통한 `손쉬운 병렬처리` 를 지원한다
- Stream은 작업을 내부 반복으로 처리한다
  - Stream을 이용한 작업이 간결할 수 있는 비결중 하나가 바로 내부 반복이다
  - 내부 반복이라는 것은 반복문을 method의 내부에 숨길 수 있다는 것을 의미한다
    - 반복문이 코드상에 노출되지 않는다

<br>

### Stream API의 동작 흐름

1. Stream의 생성
2. Stream의 중개 연산 (Stream의 변환)
3. Stream의 최종 연산 (Stream의 사용)
