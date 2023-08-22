# Synchronous vs Asynchronous

> 동기와 비동기의 차이
>
>
> -> 순서와 결과(처리)의 관점
>

<br>

### Synchronous (동기)

- 작업을 요청한 후, 해당 작업의 결과가 나올 때까지 `기다린 후 처리`  하는 것으로, I/O 작업에 대한 `readiness` 를 기다린다
  - 특정 I/O 작업을 하기 위한 준비가 되었는지에 집중하는 것

<br>

### Asynchronous (비동기)

- `작업을 요청해 놓고, 다른 일을 하다가` 해당 작업이 완료되면 그 때 완료되었음을 통지받고, 그에 따른 작업을 처리하는 것을 말한다
- 운영체제 단계의 비동기 API를 통해 이루어지며, I/O 작업이 완료되면, 그에 적합한 handler를 이용해 처리를 한다

<br>

### Synchronous (동기) vs Asynchronous (비동기)

- system call 의 완료를 `기다리면` synchronous
- system call 의 완료를 `기다리지 않으면` asynchronous
