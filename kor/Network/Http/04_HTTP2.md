# HTTP/2

> HTTP 2.0 에서 달라진 점
>

<br>

### HTTP/1 이 느린 이유

앞에서 날렸던 요청의 응답을 받아야만 다음 요청이 처리될 수 있다

>
>
- `HTTP 1.0` 버전에서만 하더라도, request를 날릴 때마다 `connection` 을 새로 생성했다 → `비효율적`
- `HTTP 1.1` 에서는 `지속 커넥션` 과 `HTTP 파이프라이닝` 이라는 개념이 들어갔다
  - 커넥션을 `재사용` 할 수 있고,
  - request를 미리 서버에 여러개 날릴 수 있게 되었다
- but, request를 `보낸 순서대로` response를 받을 수 있다는 지점에서 문제가 발생했다
  - 만약 처음에 요청한 request에 문제가 있어서 응답이 늦어지면, 그 이후에 요청한 request의 응답도 같이 늦어진다는 문제점이 발생한다

        → `Head of Line Blocking`

    - Network에서 packet `대기열` 이 존재할 때, 앞선(head) packet이 `지연`될 때 발생하는 `성능 저하 현상`

<br>

### HTTP/2 의 특징

- HTTP `header` data `압축`
  - 이전 header의 내용과 `중복`되는 `field` 를 재전송하지 않도록 하여, 데이터를 절약한다
  - 기존에 header가 `Plain Text (평문)` 이었지만, HTTP/2에서는 `HPACK` 이라는 header 압축방식을 사용하여 데이터 `전송 효율` 을 높였다
- `Server Push`
  - client가 요청하지 않은 JS, CSS, image 파일 처럼 같이 필요하게 될 특정 파일들을 server에서 `단일 HTTP 요청`  응답 시 `함께 전송` 할 수 있다
- `HTTP 1.x` 의 `Head of Line Blocking` 문제 해결
  - HTTP/2에서는 여러 파일을 한번에 `병렬 전송` 하여 전송 시간을 절감했다
  - TCP 연결 하나로 여러 요청과 응답들을 `병렬적` 으로 보낼 수 있다
    - 하나의 `connection`에서 여러 병렬 `stream` 이 존재할 수 있다
    - stream이 뒤섞여서 전송될 경우, stream number를 이용하여 수신측에서 `재조합` 된다
- `stream 우선 순위`
  - 여러 stream의 `frame` 을 `다중화 (multiplexing)` 할 수 있게 되면서, stream의 우선순위를 지정할 필요가 생겼다
  - client는 우선 순위 지정을 위해 `우선 순위 지정 트리` 를 사용하여 server의 stream 처리 우선순위를 지정할 수 있다
    - 서버는 우선순위가 높은 응답이 client에 우선적으로 전달될 수 있도록 대역폭을 설정한다
