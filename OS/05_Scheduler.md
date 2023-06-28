# Scheduler

<br>

## Process Scheduling을 위한 Queue의 종류 (3가지)

- `Job Queue`
  - 현재 시스템 내에 있는 모든 process의 집합
- `Ready Queue`
  - 현재 메모리 내에 있으면서 CPU를 잡아서 실행되기를 기다리는 process의 집합
- `Device Queue`
  - Device I/O 작업을 대기하고 있는 process의 집합

<br>

## Scheduler의 종류

### 장기 스케줄러 (Job scheduler)

> 메모리는 한정되어 있는데 많은 프로세스들이 한꺼번에 메모리에 올라올 경우, 대용량 메모리 (일반적으로 디스크)에 임시로 저장된다
>
>
> → 이 pool에 저장되어 있는 process 중, `어떤 process에 메모리를 할당하여 ready queue로 보낼지 결정` 하는 역할을 한다
>
- `메모리` 와 `디스크` 사이의 스케줄링을 담당한다
- process에 memory를 비롯한 각종 리소스를 할당한다 (admit)
- 실행중인 프로세스의 수를 제어한다
- 프로세스의 상태를 new → ready (in memory)로 바꾼다
- 참고)
  - memory에 프로그램이 너무 많이 올라가도, 너무 적게 올라가도 성능이 좋지 않은 것이다.
  - 참고로 time sharing system에서는 장기 스케줄러가 없다
    - 그냥 곧바로 memory에 올라가 ready 상태가 된다

<br>

### 단기 스케줄러 (CPU scheduler)

- `CPU`와 `메모리` 사이의 스케줄링을 담당
- `Ready Queue` 에 존재하는 process 중에 어떤 process를 running 시킬지 결정
- Process에 `CPU를 할당`
  - scheduler dispatch
- 프로세스의 상태를 ready → running → waiting → ready로 변경시킨다

<br>

### 중기 스케줄러

> Swapping!
>

- 여유 공간 마련을 위해 process를 통째로 메모리 → 디스크로 쫓아냄 (`swapping`)
- process 에게서 memory를 deallocation
  - process에서 memory 할당을 해제한다!!
- 현 시스템에서 메모리에 너무 많은 프로그램이 동시에 올라가는 것을 조절하는 스케줄러
- 프로세스의 상태를 ready → suspended로 바꾼다
  - `Process state - suspended 란?`
    - 외부적인 이유로 process의 수행이 정지된 상태로, memory에서 내려간 상태를 의미한다
    - process 전부 디스크로 `swap out` 된다
    - `Blocked` 상태는 다른 I/O 작업을 기다리는 상태이기 때문에, 스스로 ready로 돌아갈 수 있지만,
      - 이 상태는 외부적인 이유로 suspending 되었기 때문에 스스로 돌아갈 수 없다
