# @SecondaryTable

### 설명

- JPA에서 entity class가 여러 table에 mapping 되는 경우 샤용하는 annotation
- 하나의 entity가 여러 table 과 mapping 되어 있을 때 추가적인 table을 정의하고 mapping 할 수 있다

### 속성

- `name`
  - 매핑할 다른 테이블 이름 지정
- `pkJoinColumns`
  - 매핑할 다른 테이블의 기본 키를 연결하는 JOIN column 지정
- `uniqueContraints`
  - unique 제약 조건 지정
