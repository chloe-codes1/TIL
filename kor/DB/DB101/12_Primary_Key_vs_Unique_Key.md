# Primary key vs Unique key

<br>

### Primary key

- 테이블에 하나밖에 없는 key
- 테이블 내의 각 record를 고유하게 식별하는 데 사용된다
  - 그 역할을 위해 `Unique` & `Not Null` 속성을 갖고 있다
- 테이블 내에서 한 개의 row 또는 여러개의 row로 구성될 수 있다
- 여러 row로 구성된 경우 `Composite Primary Key (복합 기본 키)` 라고 한다
- Primary Key는 자동으로 `Index`를 생성하며, 이는 record를 빠르게 검색하고 관리하는 데 도움이 된다

<br>

### Unique key

- 중복을 허용하지 않는 역할을 한다 (`Unique`)
  - 각 record를 식별할 수 있다
- Null 허용
  - 해당 row가 중복되지 않으면 Null 값이 여러개 있을 수 있다는 것을 의미한다
- 한 테이블 내에서 여러개의 Unique Key를 정의할 수 있다
- Primary Key가 정의되어 있다면, 해당 row는 자동으로 Unique Key가 된다
  - but, 그 반대는 성립하지 않는다
    - Unique Key가 Primary Key 역할을 대체할 수 없다!
