# Blocking vs Non-blocking

> Blocking과 Non-blocking
>
>
> → 제어의 관점

<br>

### Blocking

- I/O가 끝날 때까지 기다리는 것
  - why?
    - 끝나기 전에는 함수가 return 되지 않기 때문이다
- 커널이 작업을 완료하기 전까지 유저 프로세스는 `작업을 중단한 채 대기` 행한다
- I/O 작업이 CPU 자원을 거의 쓰지 않기 때문에 blocking 방법은 `CPU 자원 낭비가 심하다`
- `동기화를 위해 blocking을 한다`

<br>

### Blocking vs Synchronous

- 시스템의 반환을 기다리는 동안 `대기 큐에 머무는 것이 필수가 아니면` synchronous
- 시스템의 반환을 기다리는 `동안 대기 큐에 머무는 것이 필수이면` blocking

<br>

### Non-blocking

- Blocking 방식의 비효율성을 극복하고자 만들어진 것
- I/O 작업을 진행하는 동안 유저 프로세스의 작업을 중단시키지 않는다
- 유저 프로세스가 I/O를 처리하기 위해 커널에 함수를 호출 (`system call` ) 하면, 커널에서 함수의 진행 상황과 상관 없이 바로 결과를 반환한다
  - 이 때 반환되는 결과는 반환하는 순간에 가져올 수 있는 `데이터` 에 해당한다
  - 처음에는 가져올 수 있는 데이터가 없겠지만, 시간이 지나면서 가져올 수 있는 데이터가 생겨난다
- 문제점
  - 클라이언트가 따로 반환되는 값이 원하는 사이즈가 되었는지 계속해서 `확인해줘야 한다` 는 것이다 (`polling`)
    - 반환되는 데이터가 준비되었는지 (원하는 값이 되었는지) 확인하는 과정에서 수많은 클라이언트의 요청이 동시 다발적으로 일어날 경우, `CPU에 적지 않은 부담`이 될 수 있다

<br>

### Non-blocking vs Asynchronous

- system call이 반환될 때 `실행된 결과 (데이터)와 함께 반환`될 경우 non-blocking
- system call이 반환 될 때 `실행된 결과 (데이터)와 함께 반환되지 않는` 경우 asynchronous
- 정리
  - 비동기 방식은 데이터를 콜백 함수 또는 이벤트, signal로 전달하게 되는 것
  - Non-blocking 방식은 매 system call return에 데이터가 포함되어, return 되는 데이터가 요청한 데이터가 전부 도달했는지를 파악하게 된다

<br>

### Blocking vs Non-blocking

- 애플리케이션 실행 시 운영체제 `대기 큐에 들어가`면서 요청에 대한 `system call이 완료된 후`에 응답을 보낼 경우 `blocking`
- 애플리케이션 실행 시 운영체제 `대기 큐에 들어가지 않고` 실행 여부와 관계 없이 `바로 응답` 을 보낼 경우 `non-blocking`

<br>

### 정리

- Blocking vs Non-Blocking → `제어의 관점`
- Sync vs Async → `순서와 결과(처리)의 관점`
