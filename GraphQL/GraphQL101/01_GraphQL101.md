# Intro to GraphQL

> GraphQL 시작하기!
>
> <https://tech.kakao.com/2019/08/01/graphql-basic/>
>
> <https://www.slideshare.net/shilpe34/typescript-200-graphql-179690400>

<br>

<br>

## GraphQL 이란?

> API를 위한 Query Language!

- SQL (Structured Query Language) 와 마찬가지로 Query Language
  - but, 언어적 구조 차이가 크다
    - 그 결과 이 둘에 대한 활용을 다르게 하게 됨
    - **사용 목적**
      - `sql` : **DB** 에 저장된 데이터를 효율적으로 가져오는 것이 목적
      - `gql` : **Web Client** 가 데이터를 **서버로부터** 효율적으로 가져오는 것이 목적
    - **호출**
      - `sql` : **Backend** system 에서 작성하고 호출
      - `gql` : **Client** system 에서 작성하고 후출
- 단일 요청으로 많은 데이터를 불러 올 수 있다
- 타입 시스템
- 강력한 개발자 도구 제공

<br>

<br>

### Serverside GraphQL application

- `gql` 로 작성된 쿼리를 입력으로 받아, 쿼리를 처리한 결과를 다시 **client** 로 돌려줌
- GraphQL 서버

<br>

<br>

### REST API 와 GraphQL API 의 차이점

- #### REST API

  - `URL`, `METHOD` 등으로 조합하기 때문에 다양한 Endpoint 가 존재
    - 각 Endpoint 마다 Database SQL query가 달라짐

- #### gql API

  - 단 하나의 Endpoint가 존재
  - 불러오는 데이터의 종류를 쿼리의 조합을 통해 결정
    - **gql schema type** 마다 Database SQL query가 달라짐

<br>

*구성된 인프라, 비즈니스 모델, 사용하는 목적에 따라 각각의 장단점이 바뀐다!*

<br>

<br>

### schema / type

<br>

ex)

```
type Character {
    name: String!
    appearIn: [Episode!]!
}
```

- `Object type` : Character
- `Field` : name, appearIn
- `Scala type` : String, Id, Int 등
- `!` : 필수 값 (non-nullable)
- `[ ,]` : 배열 (array)

<br><br>

### Resolver

- gql 쿼리문 파싱은 대부분의 gql 라이브러리에서 처리함
  - but, data를 가져오는 구체적인 과정은 `resolver` 가 담당하고, 직접 구현해야 함!
- 만약 field가 `스칼라 값` (문자열이나 숫자 같은 **primitive** type) 인 경우 실행이 종료됨
  - 즉, 더 이상의 연쇄적인 resolver 호출이 일어나지 않음

<br>

<br>
