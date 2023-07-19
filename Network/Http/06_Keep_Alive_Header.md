# Keep-Alive Header

<br>

### Keep Alive 란?

- HTTP protocol에서 client와 server 간 여러 요청과 응답을 `하나의 TCP 연결` 을 통해 처리할 수 있게 한다
  - HTTP는 요청을 보낼 때마다 client와 server 간 새로운 TCP 연결을 설정하고, 응답을 받은 후에 연결을 닫는 방식으로 동작한다
    - 이로 인해 요청마다 연결을 설정하고 해제하는 overhead가 발생하므로, 많은 요청을 처리해야 하는 경우 성능 저하를 초래할 수 있다
  - Keep-Alive는 이 문제를 해결하기 위해 도입된 매커니즘으로, client와 server 간의 연결을 유지하고 여러 요청과 응답을 동일한 연결을 통해 처리할 수 있게 한다
  - client가 요청을 보낼 때 `"Connection: keep-alive"` header를 포함시키면, server는 연결을 닫지 않고 여러 요청에 대해 응답을 계속 보낼 수 있다
- `HTTP/1.1` 부터는 이미 연결되어 있는 TCP 연결을 `재사용`  하는 `Keep-Alive` 라는 기능을 Default로 지원한다
- `3-ways-handshake` 과정이 생략되므로 `성능 향상` 을 기대할 수 있다
  - 연결 설정과 해제에 따른 overhead 감소 및 network 지연 시간을 줄여 성능을 향상 시킬 수 있다

<br>

### Keep Alive 특징

- Keep-Alive `유지 시간`은 연결된 `socket` 에 I/O access가 마지막에 `종료된 시점부터 정의된 시간`까지 access 가 없더라도 `session` 을 유지하는 구조이다
  - 즉, 정의된 시간 내에 access 가 이루어 진다면 계속 연결된 상태를 유지할 수 있게 된다
- Keep-Alive header를 사용하기 위해서는 Connection header는 `keep-alive` 로 설정되어야 한다
  - but, HTTP/2에서는 무시되고, 연결 관리는 해당 프로토콜 내에서 다른 매커니즘에 의해 처리된다
- `Event-driven` 구조여서 `non-blocking`을 사용하는 `Nginx` 등은 `Keep-Alive`를 하면서도 `Thread`를 점유하지 않기 때문에 `동시 처리`에 유리하다

<br>

### Keep-Alive timeout을 설정하는 이유

- 서버 자원은 무한정이 아니다
- 접속을 계속 유지하는 것은 server에 손실을 발생시킨다
- 즉, server와 연결을 맺을 수 있는 `socket` 은 한정되어 있고, 연결이 오래 지속되면 다른 사람들이 연결을 못하게 되는 상황이 닥친다

<br>

### HTTP/1.0+ 와 HTTP/1.1 에서의 Keep-Alive

- `1.0+`에서는 Keep-Alive를 `사용하기 위해` 설정을 해야했다면,
- `1.1`에서는 Keep-Alive를 `끊기 위해` 설정을 해야한다
- 즉, 설정의 목적이 사용하기 위함이냐 끊기 위함이냐로 생각하면 된다!
