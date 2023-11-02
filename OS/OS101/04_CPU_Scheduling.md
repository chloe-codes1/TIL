# CPU Scheduling

## CPU and I/O Bursts in Program Execution

<p align="center" width="100%">
  <img width="330" alt="CPU and I/O Bursts in Program Execution" src="https://github.com/chloe-codes1/TIL/assets/53922851/e3d3bdbc-5d81-4016-9090-cc3974ec6edc">
</p>

## CPU-burst Time의 분포

<p align="center" width="100%">
  <img width="426" alt="CPU-burst Time" src="https://github.com/chloe-codes1/TIL/assets/53922851/d95a74c6-60fc-41f7-84b1-3adba67fbd97">
</p>

## Process 의 특성 분류

Process는 그 특성에 따라 다음 두 가지로 나눈다

- `CPU bound job`
  - CPU를 길게 쓰고, I/O를 짧게 쓰는 작업
    - few very log CPU bursts
  - 계산 위주의 job
  - ex) 과학적 연산 등 연산이 오래 걸리는 작업을 수행하는 경우
- `I/O bound job`
  - CPU를 짧게 쓰고, I/O를 길게 쓰는 작업
    - many short CPU bursts
  - CPU를 잡고 계산하는 시간보다 I/O에 많은 시간이 필요한 job
  - ex) 사람과 Interaction을 많이 하는 경우

### CPU Scheduling의 필요성

- 여러 종류의 job(=process)이 섞여 있기 때문에 CPU Scheduling 이 필요하다
  - Interactive job에게 적절한 response 제공 요망
    - 사람과 Interaction을 하는 job
  - CPU와 I/O 장치 등 system 자원을 골고루 효율적으로 사용
- I/O bound job이 CPU를 빨리 얻을 수 있도록 하는 목적
  - CPU를 먼저 주어야 빨리빨리 CPU를 쓰고 나가기 때문
  - 사람과 interaction 하기 때문에 빠른 응답성 제공 필요
  - 쓰고 나서는 바로 I/O 작업이 아루어지는데, CPU를 못주고 있으면

## CPU Scheduler & Dispatcher

### CPU Scheduler

- 운영체제 코드 중 CPU scheduling을 하는 code
- Ready 상태의 process 중에서 CPU를 줄 process를 고른다

### Dispatcher

- CPU의 제어권을 CPU Scheduler에 의해 선택된 process에게 넘긴다
- 이 과정을 context switch 라고 한다

### CPU Scheduling이 필요한 경우

Process에게 다음과 같은 상태 변화가 있는 경우

1. Running → Blocked (e.g. I/O 요청하는 system call)
2. Running → Ready (e.g. 할당 시간 만료로 timer interrupt)
3. Blocked → Ready (e.g. I/O 완료 후 interrupt)
4. Terminate

→ 1, 4 에서의 scheduling은 `nonpreemptive` (= 강제로 빼앗지 않고 자진 반납)

→ 그 외 다른 scheduling은 preemptive (= 강제로 빼앗음)

## Scheduling Criteria

> Performance Index (= Performance Measure, 성능 척도)
>
- **CPU Utilization (이용률)**
  - keep the `CPU as busy as possible`
  - CPU를 놀게 하지 않고 이용률은 높을 수록 좋다
- **Throughput (처리량)**
  - `number of processes` that `complete` their execution per time unit
  - 처리량은 많을수록 좋다
- **Turnaround Time (소요 시간, 반환 시간)**
  - amount of time to `execute a particular process`
  - CPU burst를 하고 나서, I/O burst를 하러 나가기까지 전체 시간
    - ready queue에서 기다린 시간 + 실제로 CPU를 쓴 시간
- **Waiting Time (대기 시간)**
  - amount of time a process has been `waiting in the ready queue`
  - 처음으로 기다리는 시간이 아닌, CPU를 쓰러 와서 기다린 전체 시간의 합
- **Response Time (응답 시간)**
  - amount of time it takes `from when a request was submitted until the first response is produced`, not output
  
      (for time-sharing environment)

  - CPU를 쓰러 들어와서 처음 쓰기까지의 시간을 뜻함
    - process가 시작해서 처음 CPU를 쓰기 까지의 시간 아님!!

## Scheduling Algorithms

### FCFS (First-Come First-Served)

- 설명
  - ready queue에 먼저 들어온 process 순으로 실행한다
- 문제점
  - `Convoy effect (호위 효과)`
    - short process behind long process
    - 오래 걸리는 process가 먼저 도착해서 CPU를 오래 쓰는 탓에 짧게 걸리는 process가 오래 걸리게 되는 것

### SJF (Shortest Job First)

- 설명
  - 각 process의 다음번 CPU burst time 을 가지고 scheduling에 활용
  - CPU burst time이 가장 짧은 process를 제일 먼저 schedule
    - CPU를 가장 짧게 쓰려는 job에게 제일 먼저 CPU를 주는 것
- 종류

    > Two schemes
    >
  - `Non-preemptive (비선점)`
    - 일단 CPU를 잡으면 CPU burst가 완료될 때까지 CPU를 선점 (preemption) 당하지 않음
  - `Preemptive (선점)`
    - 현재 수행중인 process의 남은 burst time 보다 더 짧은 CPU burst time을 가지는 새로운 process가 도착하면 CPU를 빼앗김
    - 이 방법을 `Shortest-Remaining-Time-First (SRTF)` 라고도 부름
- 특징
  - SJF is `optional`
    - 주어진 process들에 대해 `minimum average waiting time` 을 보장한다
    - 대기 시간 측면에서 최적이다
  - A priority number (integer) is associated with each process
    - high priority를 가진 process에게 CPU 할당
      - (smallest integer = high priority)
  - SJF는 일종의 priority scheduling이다
    - `priority = predicated next CPU burst time`
- 문제점
  - `Starvation`
    - low priority processes may never executed
  - `Aging`
    - as time progresses increase the priority of the process
- 다음 CPU Burst Time 의 예측

    > 다음번 CPU burst time을 어떻게 알 수 있을까? (input data, branch, user …)
    >
  - 추정만이 가능하다
  - 과거의 CPU burst time을 이용해서 추정 (exponential averaging)
