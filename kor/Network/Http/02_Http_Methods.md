# Http Methods

> Http method 별 특징

<br>

- `GET`
  - 특정 리소스를 가져오도록 요청한다
  - GET 요청은 데이터를 가져올 때만 사용해야 한다
- `POST`
  - 서버로 데이터를 전송한다
  - Request Body의 유형은 `Content-Type` header로 나타낸다
  - PUT과 POST의 차이는 멱등성으로, `PUT`은 `멱등성`을 가진다
    - PUT은 한 번을 보내도, 여러 번을 보내도 같은 효과를 보인다 (side effect x)
  - Message body를 통해 서버로 데이터를 전달
  - 신규 리소스를 `생성`할 때 주로 사용
- `PUT`
  - 요청 payload를 사용해 `새로운 리소스를 생성`하거나, 대상 리소스를 나타내는 `데이터를 대체`한다
  - `멱등성`을 가진다
- `PATCH`
  - 리소스를 `일부만 수정`할 때에 사용된다
  - 멱등성 x
  - PATCH나 POST은 다른 리소스에 side-effect를 일으킬 가능성이 있다
- `DELETE`
  - 지정한 리소스를 삭제한다
- `HEAD`
  - 특정 리소스를 GET method로 요청했을 때 돌아올 Header를 요청한다
  - HEAD method에 대한 응답은 Body를 가져선 안되며, Body가 존재하더라도 무시해야한다
  - Web service의 health check나 web server 정보를 얻기 위해 사용
- `OPTIONS`
  - 목표 리소스와의 통신 option을 설정하기 위해 사용된다
- `TRACE`
  - `loopback`test 위해 사용된다
- `CONNECT`
  - 요청한 리소스에 대해 `양방향 연결` 을 시작하는 method
    - 터널을 열기위해 사용될 수 있다
  - ex) SSL (HTTPS)을 사용하는  web site에 접속하는데 사용될 수 있다
    - Client는 원하는 목적지와의 TCP 연결을 HTTP proxy server에 요청한다
    - 그러면 server는 client를 대신하여 연결의 생성을 진행한다
    - 한번 서버에 의해 connection이 맺어지면, proxy server는 client에 오고가는 TCP stream을 계속해서 proxy한다
