# GraphQL Korea Meetup on 6/13/2020

<br>

<br>

## 1. Relay with Python

> 발표자: 재현님~~~~!!! ㅎ_ㅎ
>
> *"예측가능한 일관성이 주는 뜻밖의 효율성"*

<br>

### Graphene

- ORM 방식으로 정의하면 GraphQL Schema로 바꾸어 줌
- GraphQL 을 객체화해서 잘 만들어준다!

<br>

#### Relay

> Graphene 은 `Relay` 를 지원한다
>
> **Relay**
>
> : GraphQL 기반 데이터 중심 React application을 구축하기 위한 JavaScript framework

- Node
  - `graphene.relay` 에서 제공하는 interface
  - `ID!` field 하나만을 갖는다
- Connection
  - slicing과 pagination을 제공하는 향상된 버전의 리스트
    - Graph에 분산되어 있는 각 점을 **Node**라고 하며, 데이터 구조를 구성하는 하나의 개체를 의미하고,
    - 서로 연관된 **Node** 를 연결하는 선은 **Edge** 라고 한다
      - GraphQL에서 각 Node 의 주소를 **Cursor**라고 하고,
        - **Connection**은 **Cursor**를 기반으로한 `pagination` design pattern
  - ex)
    - `relay.Connection`
    - `relay.ConnectionField`
- Mutations
  - 데이터 수정 작업을 하는 Mutation을 Graphene에서는 subclass `relay.ClientIDMutation`을 통해 쉽게 관리할 수 있다

<br>

### Graphene-Django

> [Docs](https://docs.graphene-python.org/projects/django/en/latest/)

- GraphQL을 Django 에서 쉽게 적용 가능하도록 도와줌

<br>

<br>

## 2. GraphQL을 언어로써 다루는 방법

> 발표자: 김혜성님
>
> *"오늘 날 GraphQL은 API 구현 뿐 아니라 강력한 "모델링 언어"로써 활약하고 있습니다. GraphQL 언어를 자바스크립트로 다루는 방법과 이를 확장하는 다양한 사례들을 소개합니다."*

<br>

### Document

- GraphQL AST 의 최상위 노드
- 하위에 대한 다양한 Definition을 포함하고 있음

<br>

<br>

### Definition

- Executable Definition
  - Query / Mutation / Fragment etc.
- Other Definition
  - Client 개발자에게 친숙한 그 부분..ㅎ

<br>

<br>

### SDL (Schema Definition Language)

> 강력한 범용 모델링 언어

- 방향성 순환 그래프
- 타입 시스템 기반 검증
- Interface / Union 을 통한 다형성 지원
- 확장 가능성
- 매크로

<br>

<br>

### Schema vs ExecutableSchema

<br>

- 몇 가지 전처리 작업을 거쳐 `런타임` 을 추가함
  - Resolvers
  - Directives
    - GraphQL Document 처리기에 추가적인 정보를 제공할 수 있는 지시자
      - Standard (`@deprecated`, `@include`, `@skip`)
      - Schema Directive
        - ex) `@deprecated`
      - Operational Directive
        - ex) `@include`, `@skip`

<br>

<br><br>

`+`

#### 느낀점

- GraphQL 에 관심이 더 생겼다!!!!!!
- 더 깊게 공부해봐야겠다 넘 재밌다!
