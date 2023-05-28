# TreeSet, TreeMap vs HashSet, HashMap
>
> 어떤 상황에서 어떤 자료구조를 써야할까!

<br>

### TL;DR

- 특별한 사유가 없다면 `검색 성능`이 좋은 `HashMap`을 사용
- `순서를 보장`하고 싶다면 LinkedHashMap을 사용
- 키값을 일정하게 `iterate` 하고자한다면 `TreeMap`을 사용

<br>

### TreeMap과 HashMap의 차이점

- TreeMap은 HashMap과 유사한 자료 구조이지만, TreeMap은 데이터가 정렬되어 있다는 점이 다르다
- HashMap은 데이터가 정렬되어 있지 않기 때문에, TreeMap보다 데이터 검색 속도가 느릴 수 있다
- but, HashMap은 TreeMap보다 메모리 사용량이 적다

<br>

### 순서 보장 측면

- `HashMap`은 순서를 보장하지 않는다
  - `LinkedHashMap` 은 입력된 순서를 보장한다!
- `TreeMap`은 Key 값으로 사용된 클래스의 비교 연산을 활용하여 순서를 보장한다
  - key 값에 따라 자동으로 `sort` 되는 방식

<br>

### 속도 측면

- `HashMap` 의 시간 복잡도는 `O(1)` 이다
  - `해시 값`을 사용하기 때문
- `TreeMap` 의 시간 복잡도는 `O(log n)` 이다
  - 대신, `정렬된 순서`를 얻을 수 있다

<br>

### Key에 `null` 허용 여부

- `HashMap` 은 key에 null `허용`
- `TreeMap` 은 key에 null `허용 X`

<br>

### TreeMap은 언제 쓰지?

- 순서가 있는 데이터를 저장하고 검색해야 하는 경우
  - 동기화 처리가 되어있어 `Thread-safe` 하다
- 데이터를 정렬된 순서대로 검색해야 하는 경우
- 데이터에 대한 삽입, 삭제, 검색 연산이 자주 수행되는 경우

<br>

### TreeMap이 효율적이지 않은 경우

- 데이터의 크기가 매우 큰 경우
- 데이터에 대한 삽입, 삭제, 검색 연산이 자주 수행되지 않는 경우
