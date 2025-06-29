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

### Priority Scheduling

> A priority number (integer) is associated with each process
>
- 특징
  - `highest priority` 를 가진 process에게 CPU를 할당
    - smallest integer == highest priority
  - SJF는 일종의 priority scheduling이다
- 문제점
  - `Starvation` : low priority process may never execute
- 해결
  - `Aging` : as time progresses, increase the priority of the process

### Round Robin (RR)

- 특징
  - 각 process 는 동일한 크기의 할당 시간 (time quantum) 을 가진다
    - 일반적으로 10 - 100 ms
  - 할당 시간이 지나면 process는 선점당하고, ready queue의 제일 뒤에 가서 다시 줄을 선다
  - n개의 process가 ready queue에 있고, 할당 시간이 q time unit인 경우, 각 process는 최대 q time unit 단위로 CPU 시간의 1/n을 얻는다

        → 어떤 process도 (n-1)q time unit 이상 기다리지 않는다

- Performance
  - q large → FCFS
  - q small → `context switch` overhead가 커진다
- 장점
  - 일반적으로 SJF보다 average turnaround time이 길지만, `response time` 은 더 짧다

### Multilevel Queue

- Ready queue를 여러개로 분할
  - `foreground`
    - interactive job
  - `background`
    - batch job (no human interaction)
- 각 queue는 독립적인 scheduling algorithm을 가짐
  - `foreground`
    - RR
  - `background`
    - FCFS
- Queue에 대한 scheduling이 필요

    > 각 queue 마다 wait을 주는 것
    >
  - **Fixed priority scheduling**
    - 두 개의 우선 순위 그룹을 나눈다 (foreground, background)
    - serve all from foreground then from background
      - foreground에 속한 process들이 먼저 모두 실행되고 나면, 그 다음에 background group에 속한 process들을 실행한다
    - possibility of starvation
  - **Time slice**
    - 각 queue에 CPU time을 적절한 비율로 할당
    - e.g.
      - 80% to foreground in RR
      - 20% to background in FCFS
- Priority 별 queue 분배

  <img width="939" alt="image" src="https://github.com/chloe-codes1/TIL/assets/53922851/b0d90c74-43d8-4df6-8213-868c5e588afc">

  한번 정해진 queue는 바뀌지 않는다

### Multilevel Feedback Queue

- Process가 다른 queue로 이동 가능
  - 상위 queue가 우선순위가 높다
  - 상위 queue가 비어야 하위 queue가 채워진다
- aging을 이와 같은 방식으로 구현할 수 있다
  - aged job을 상위 queue로 보내기
- Multilevel feedback queue scheduler 를 정의하는 Parameters
    1. Queue의 수
    2. 각 queue의 scheduling algorithm
    3. Process를 상위 queue로 보내는 기준
    4. Process를 하위 queue로 내쫓는 기준
    5. Process가 CPU 서비스를 받으러 할 때, 들어갈 queue를 결정하는 기준
- e.g.

  <img width="882" alt="image" src="https://github.com/chloe-codes1/TIL/assets/53922851/bb011162-f164-4187-9a4a-659f51793655">

- Three queues
  - Q0 - time quantum 8 ms
  - Q1 - time quantum 16 ms
  - Q2 - FCFS
- Scheduling Flow
  - new job이 queue Q0로 들어감
  - CPU를 잡아서 할당 시간인 8ms 동안 수행됨
  - 8ms 동안 다 끝내지 못했으면 Q1으로 내려감
  - Q1에 줄서서 기다리다가, CPU를 잡아서 16ms 동안 수행됨
  - 16ms 안에 끝내지 못한 경우 Q2로 쫓겨남

### Multiple-Processor Scheduling

- CPU가 여러 개인 경우 scheduling은 더욱 복잡해짐
- `Homogeneous process` 인 경우

    > 누구나 처리할 수 있는 역량이 똑같은 CPU
    >
  - Queue에 한줄로 세워서 processor가 알아서 꺼내가게 할 수 있다
  - but, 반드시 특정 processor에서 수행되어야 하는 process가 있는 경우에는 문제가 더 복잡해진다
- `Load sharing` (= Load balancing)
  - 일부 processor에 job이 몰리지 않도록 부하를 적절히 공유하는 메커니즘 필요
  - 별개의 queue를 두는 방법 vs 공동 queue를 사용하는 방법
- `Symmetric Multiprocessing (SMP)`
  - 각 processor가 각자 알아서 스케줄링 결정
  - 균일한 작업을 여러곳에서 할 때는 조율하는 processor가 없는게 효율적일 수도 있다
- `Asymmetric multiprocessing`
  - 하나의 processor가 system data의 접근과 공유를 책임지고, 나머지 processor는 거기에 따름

### Real-Time Scheduling

- `Hard real-time systems`
  - 정해진 시간 안에 반드시 끝내도록 scheduling 해야 함
  - 그러기 위해 process들의 CPU 도착 시간을 미리 알고 scheduling 하는 경우도 있다 (off-line scheduling)
    - ↔ online scheuluing
      - system이 실행중에 동적으로 process를 scheduling
      - 작업이 도착하는 시점에서 결정을 내릭 때문에, 실행 시점에 알려진 정보만 사용할 수 있다
- `Soft real-time computing`
  - 일반 process에 비해 높은 priority를 갖도록 해야 함
  - e.g. 동영상이 끊기지 않도록 동영상 재생 process가 먼저 CPU를 얻을 수 있도록 priority를 높이기

### Thread Scheduling

> 하나의 process 안에 CPU 수행 단위가 여러개 있는 것
>
- `Local Scheduling`
  - **User level thread**의 경우 사용자 수준의 thread library에 의해 어떤 thread를 scheduling 할지 결정
- `Global Scheduling`
  - **Kernel level thread**의 경우 일반 process와 마찬가지로, kernel의 단기 scheduler가 어떤 thread를 scheduling 할지 결정

## Algorithm Evaluation

- `Queueing models`
  - 확률 분포로 주어지는 arrival rate와 service rate 등을 통해 각종 performance index 값을 계산
- `Implementation & Measurement`
  - 실제 시스템에 알고리즘을 `구현` 하여 실제 작업에 대해서 성능을 `측정` 하여 비교
- `Simulation`
  - 알고리즘을 모의 프로그램으로 작성 후 `trace` 를 입력으로 하여 결과 비교
  - trace 란?
    - simulation의 input이 되는 data
    - 신빙성이 있어야함 (실제 프로그램의 동작을 대변할 수 있어야 함)
