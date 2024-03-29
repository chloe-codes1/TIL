# RESTful API

> RESTful한 API란?
>

<br>

### REST 특징

- `client-server 구조`
  - 클라이언트는 유저와 관련된 처리를,
  - 서버는 REST API를 제공함으로써
  - 각각의 `역할`이 확실하게 `구분`되고 `일관된 인터페이스`로 `분리`되어 작동할 수 있게 한다
- `무상태성 (stateless)`
  - REST는 HTTP의 특성을 이용하기 떄문에 `무상태성`을 갖는다
  - 서버에서 어떤 작업을 하기 위해 `상태 정보`를 기억할 필요가 없고, 들어온 요청에 대해 처리만 해주면 되기 때문에 구현이 쉽고 단순해진다
- `캐시 처리 가능 (cacheable)`
  - 대량의 요청을 효율적으로 처리하기 위해 캐시가 요구된다
  - 캐시 사용을 통해 응답시간이 빨라지고 REST Server 트랜잭션이 발생하지 않기 때문에 전체 응답시간, 성능, 서버의 자원 이용률을 향상 시킬 수 있다
- `유니폼 인터페이스 (Uniform)`
  - `Http 표준`에만 따른다면 `모든 플랫폼`에서 사용이 가능하며, `URI`로 지정한 리소스에 대한 `조작`을 가능하게 하는 아키텍쳐
  - 즉, **특정 언어나 기술에 종속되지 않는다**

<br>

### 핵심 규칙

- URI는 정보의 자원을 표현해야 한다
- 자원에 대한 `행위`는 `HTTP Method` (GET, POST, PUT, DELETE 등)으로 표현한다

<br>

### RESTful API란?

> RESTful은 REST를 REST 답게 쓰기 위한 방법으로, 누군가가 공식적으로 발표한 것은 아니다
>

- **자원을 식별할 수 있어야 한다**
  - URL 만으로 `어떤 자원`  을 제어하려고 하는지 알 수 있어야 한다
- **행위는 명시적이어야 한다**
  - GET을 이용해서 UPDATE와 DELETE를 하는 것 → X
