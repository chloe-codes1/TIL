# Process Synchronization

<br>

## Critical Section & Critical Section Problem

### Critical Section (임계 영역)

멀티 스레딩의 문제점에서 나오듯, 동일한 자원에 동시에 접근 하는 작업 (ex. 공유하는 변수 사용, 동일 파일을 사용)을 실행하는 코드 영역 을 Critical Section 이라고 한다

<br>

### Critical Section Problem (임계 영역 문제)

- Process들이 critical section을 함께 사용할 수 있는 protocol을 설계 하는 것을 의미한다
- Requirements (해결을 위한 기본 조건)
  - `Mutual Exclusion (상호 배제)`
    - Process p1이 critical section에서 실행중이라면, 다른 process들은 p1이 가진 critical section에서 실행될 수 없다
  - `Progress (진행)`
    - Critical section에서 실행중인 프로세스가 없고, 별도의 동작이 없는 프로세스들만 critical section 진입 후보로서 참여될 수 있다
  - `Bounded waiting (한정된 대기)`
    - p1이 critical section에 진입 신청 후 받아들여질 때가지, 다른 process들이 critical section에 진입하는 횟수는 제한이 있어야 한다

<br>

## Solution

### Mutex Lock

- 동시에 공유 자원에 접근하는 것을 막기 위해 `Critical Section에 진입하는 process는 lock을 획득`하고, critical section을 `빠져 나올 때, Lock을 방출`함으로써 동시에 접근이 되지 않도록 한다
- 한계
  - 다중 처리기 환경에서는 시간적인 효율성 측면에서 적용할 수 없다

<br>

### Semaphores

> 소프트웨어상에서 임계 영역 문제를 해결하기 위한 동기화 도구
>
- 설명
  - 멀티프로그래밍 환경에서 다수의 process 나 thread 가 n 개의 공유 자원에 접근하는 것을 제한하는 방법으로 사용되는 동기화 기법
- 종류
  - `Counting Semaphore (카운팅 세마포)`
    - 가용한 개수를 가진 자원에 대한 `접근 제어`용으로 사용되며, 세마포는 그 가용한 자원의 개수로 초기화 된다
    - 자원을 사용하면 세마포가 감소, 방출하면 세마포가 증가한다
  - `Binary Semaphore (이진 세마포)`
    - `MUTEX` 라고도 부르며, 상호배제 ( Mutal Exclusion)의 머릿글자를 따서 만들었다
    - 이름 그대로 0과 1 사이의 값만 가능하며, 다중 프로세스들 사이의 Critical Section 문제를 해결하기 위해 사용한다
- 단점
  - `Busy waiting (바쁜 대기)`
    - `Spin lock` 이라고 불리는 Semaphore 초기 버전에서 Critical Section에 진입해야하는 process 는 진입 코드를 반복 실행해야하며, CPU 시간을 낭비했었다
      - 이를 Busy Waiting이라고 부르며 특수한 상황이 아니면 비효율적이다.
    - 일반적으로는 Semaphore에서 `Critical Section에 진입을 시도했지만 실패한 프로세스`에 대해 `Block`시킨 뒤, Critical Section에 자리가 날 때 `다시 깨우는 방식`을 사용한다.
      - 이 경우 Busy waiting으로 인한 시간낭비 문제가 해결된다.
  - `Deadlock (교착 상태)`
    - Semaphore가 Ready Queue를 가지고 있고,
    - 둘 이상의 process가 critical section 진입을 무한정 기다리고 있고,
    - critical section에서 실행되는 process는 진입 대기 중인 process가 실행되어야만 빠져나올 수 있는 상황을 지칭

<br>

### 모니터

- 고급 언어의 설계 구조물로서, 개발자의 코드를 `상호배제 하게`끔 만든 `추상화된 데이터 형태`
- 공유 자원에 접근하기 위한 키 획득과, 자원 사용후 해제를 모두 처리한다
  - Semaphore는 직접 키 해제와 공유자원 접근 처리가 필요하다!
