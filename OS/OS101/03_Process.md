# Process

> Reference: [이화여대 운영체제 강의 - 반효경 교수님](http://www.kocw.net/home/cview.do?cid=4b9cd4c7178db077)
>

<br>

## 프로그램의 실행 (Memory load)

- 프로그램은 파일 시스템에 실행 파일 형태로 저장되어 있다가,
- 실행시키면 해당 프로그램이 memory에 올라가서 process 가 된다
- 이때, OS Kernel은 이미 memory에 올라가 있다
- 프로그램이 실행될 때 해당 프로그램만의 독자적인 Address Space를 `Virtual Memory`에 갖는다
  - 그 중 당장 필요한 부분은 `Physical memory`에 올라가고,
  - Physical memory 에 올라가지 않은 부분은 `Swap area`  로 들어간다
  - 이 중 일부는 파일 시스템의 파일 형태로 존재한다

### Address Translation

virtual memory에 올라가 있는 주소에서 physical memory 주소로 변환이 필요하다

### Virtual Memory

- stack
  - 함수 안에 있는 지역 변수가 위치한다

      → 함수의 호출과 return과 관련된 것

- data
  - 전역 변수 / 프로그램이 시작될 때부터 종료될 때까지 있는 값이 위치한다
- code
  - 실행 파일에 있던 code가 올라오는 것
  - CPU에서 실행할 기계어가 위치

      → 컴파일 된 기계어 코드

- `Kernel Address Space`
  - Kernel도 함수 호출을 하기 때문에 동일하게 stack, data, code로 구성되어 있다

## Kernel 주소 공간의 내용

### 구조

- Kernel은 하나의 프로그램으로서 함수 구조로 이루어져 있다
- 각  Process 의 Address Space는 Code, Data, Stack으로 구성된다

### 구성 요소

- 운영체제의 `Code`

    > 주로 운영체제가 하는 일이 Kernel Code 안에 들어가 있다고 보면 된다
    >
  - System call, Interrupt 처리 코드
  - 자원 관리를 위한 코드
  - 편리한 서비스 제공을 위한 코드
- 운영체제의 `Data`
  - 모든 hardware, process 를 관리하기 위한 자료구조를 갖고 있다

      → 이것을 `PCB (Process Control Block)` 라고 한다

- 운영체제의 `Stack`
  - 지금 누가 실행중인지를 알기 위해 process의 kernel stack은 각각 저장된다

      → Kernel로 들어오기 전에 (kernel이 호출되기 전에) 어떤 process에서 실행된 것인지에 따라 구분되어 저장된다

  - Kernel의 stack이기 때문에 kernel 함수와 관련된다

## 사용자 프로그램이 사용하는 함수

- 사용자 정의 함수

    > 해당 process address space 내에 위치
    >
  - 자신의 프로그램에서 정의한 함수
  - program counter 값만 바꾸어 다른 위치의 기계어를 실행하면 된다
- 라이브러리 함수

    > 해당 process address space 내에 위치
    >
  - 자신이 프로그램에서 정의하지 않고, 가져다가 쓴 함수
  - 자신의 프로그램의 실행 파일에 포함되어 있다
- 커널 함수

    > kernel address space 내에 위치
    >
  - 운영체제 프로그램의 함수

      → 커널의 코드에 들어있는 함수

  - virtual memory의 주소 공간을 가로질러서 다른 program 의 영역으로 바뀌는 것

      → CPU 제어권을 OS에 넘긴 후 실행한다

  - 커널 함수의 호출 == `System call`

## 프로그램의 실행

### User-Defined & Library Function Call

- user mode (mode bit: 1)
- 주소 공간에 있는 code가 user mode 로 실행된다

### System Call

- kernel mode (mode bit: 0)
- CPU 제어권이 OS에게 넘어가서 Kernel mode에서 OS 주소공간에 있는 코드가 실행된다

## Process의 개념

### Process란?

실행중인 프로그램

→ *Process is a program in execution*

### Process의 문맥 (context)

> Process의 현재 상태를 나타냄
→ 시간에 따라 바뀌는 개념
>
- CPU 수행 상태를 나타내는 hardware context

    > CPU에서 어디까지 수행했는가?
    >
  - Program Counter

      → 현재 어디를 실행하고 있는가

  - 각종 register

      → Register에 어떤 값을 넣고 있었는가

- Process의 주소 공간

    > 자신의 memory 공간에 무엇을 가지고 있는가?
    >
  - code, data, stack
- Process 관련 Kernel 자료 구조
  - `PCB (Process Control Block)`
    - CPU, memory 등을 얼마나 썼는지에 대한 정보를 갖고 있는 자료구조
    - PCB를 봐야 context를 알 수 있기 때문에 process를 관리하기 위한 자료구조라 할 수 있음
  - Kernel Stack
    - process 마다 다른 kernel stack을 갖는다

## Process의 상태

> Process는 state가 변경되며 수행된다
>

### `Running`

- CPU를 잡고 instruction을 수행중인 상태
- CPU에서 기계어를 실행하는 process는 매순간 1개다
  - CPU를 잡고 있는 process를 running 상태라고 한다

### `Ready`

- CPU를 기다리고 있는 상태의 process

    (메모리 등 다른 조건은 모두 만족)

### `Blocked (wait, sleep)`

- CPU를 주어도 당장 instruction을 수행할 수 없는 상태
- Process 자신이 요청한 event (e.g. I/O) 가 만족되지 않아 이를 기다리는 상태
  - e.g. disk에서 file을 읽어와야 하는 경우
- Inturrupt 되면 진행중이던 event가 완료 되었다는 의미이므로 Ready 상태로 바꿔준다

### New

process가 생성중인 상태

### Terminated

수행(execution)이 끝난 상태

## Process 상태 변화도

<p align="center" width="100%">
  <img width="713" alt="process state" src="https://github.com/chloe-codes1/TIL/assets/53922851/8f7c73db-972e-48cc-8388-52315c0a050e">
</p>

- new
  - 생성중인 상태

      → 생성 시작이 안됐으면 process가 아님!

- ready
  - CPU만 할당되면 바로 실행이 가능한 상태
  - CPU가 필요한 부분은 memory에 올라가 있어야 함
- running
  - CPU scheduler가 dispatch를 하면 running 상태가 됨
  - running 상태가 끝나는 경우
    - Timer interrupt
      - 할당 시간 만료
      - ready queue의 제일 뒤로 가서 줄을 서야하는 상황
    - I/O or event wait
      - 오래 걸리는 작업 때문에 blocked 상태로 들어가는 경우
    - Exit
      - 종료되는 경우
- waiting (blocked)
  - 오래 걸리는 작업이 끝나면 (보통 interrupt가 걸림) 해당 process의 상태를 ready로 바꿔서 다시 CPU가 해당 process를 실행할 준비를 시켜둔다
- terminated
  - 종료중인 상태

      → 종료가 완료되면 process가 아님!

## PCB (Process Control Block)

<p align="center" width="100%">
  <img width="230" alt="pcb" src="https://github.com/chloe-codes1/TIL/assets/53922851/85034d50-fde4-4960-ace3-d8c07fe7357a" >
</pr>

### 설명

OS가 각 process를 관리하기 위해 두는 자료구조로, process 당 유지하는 정보를 뜻한다

### 구성 요소

> 구조체로 유지한다
>
- OS가 관리상 사용하는 정보
  - Process State, Process ID
  - Scheduling Information, Priority (가장 높은 process에 CPU가 할당된다)
- CPU 수행 관련 hardware 값

    > Context Switching에 대비하여 저장해 놓는 값
    >
  - Program Counter, Registers
- Memory 관련
  - code, data, stack의 위치 정보
- File 관련
  - Open file descriptors
    - file 이나 I/O resource를 고유하게 식별하는데 사용된다 (0부터 시작하여 순차적으로 할당)
    - process는 oepn file descriptor를 사용하여 파일을 읽거나 쓸 수 있다
      - file에 대한 I/O를 수행할 수 있으며, file을 열거나 닫을 때 사용된다

## Context Switching

<p align="center" width="100%">
  <img width="470" alt="context switch" src="https://github.com/chloe-codes1/TIL/assets/53922851/92eca9fc-8723-4504-b944-322acbae5088">
</p>

### 설명

CPU를 한 process에서 다른 process로 넘겨주는 과정

### 필요한 이유

- 다른 프로그램에서 CPU 그냥 빼앗아 가는게 아니라, 다시 CPU가 할당되었을 때 이어서 작업할 지점을 알 수 있게 Process Context를 설정해야 한다
- e.g. CPU가 process A에서 process B로 넘어가게 하려면, 현재 기계어의 어디를 실행중인지 등의 정보를 CPU를 뺏기 전에 process A의 PCB에 저장한 후 process B에게 CPU를 넘겨준다

### 동작

> CPU가 다른 process에게 넘어갈 때 OS는 아래의 동작을 수행한다
>
- CPU를 내어주는 process의 상태를 해당 process의 PCB에 저장
  - 현재 기계어에서 어디까지 실행했는지, register에 어떤 값을 넣어 줬었는지를 PCB에 저장한다
- CPU를 새롭게 얻는 process의 상태를 PCB에서 읽어오기

### Context Switch 구분하기

> System Call 이나 Interrupt 발생시 반드시 context switch 가 일어나는 것은 아니다
>

### context switch인 것

사용자 process A ↔ 사용자 process B

### context switch가 아닌것

사용자 process A → OS → (다시) 사용자 process A

### context switch와 overhead의 관계

- user mode에서 kernel mode로 가는건 context switch보다 상대적으로 overhead가 적은 작업이다
- CPU 수행 정보 등 context의 일부를 PCB에 저장해야 하지만, context switch 하는 경우 그 부담이 훨씬 크다 (eg. cache memory flush)

## Process를 Scheduling 하기 위한 Queue

> Process들은 각 queue들을 오가며 수행된다
>

### Job queue

현재 system 내에 있는 모든 process의 집합

### Ready queue

현재 memory 내에 있으면서 CPU를 잡아서 실행되기를 기다리는 process의 집합

### Device queues (I/O Queue)

- 오래 걸리는 작업
- I/O device의 처리를 기다리는 process의 집합

### Process Scheduling Queue 의 모습

<p align="center" width="100%">
  <img width="473" alt="process scheduling queue" src="https://github.com/chloe-codes1/TIL/assets/53922851/9fac457b-febe-4267-ab3c-11fafb653744">
</p>

- `fork a child`
  - 자식 process를 만드는 것

      → 복제 생성을 함

  - 자식에게 cpu를 넘기는게 효과적이라 자식에게 보통 할당함

## Scheduler

> OS 안에 들어있는 code의 일부다
>

### Long-Term Scheduler (job scheduler)

> OS 내에서 memory scheduling을 하는 역할
>
- 시작 process 중 어떤 것들을 ready queue로 보낼지 결정
- process에 memory (및 각종 자원)을 주는 문제
  - process가 실행될 때 `memory`에 올라오도록 하는 역할을 담당
- `Degree of Multi-programming` 을 제어
  - Degree of Multi-programming 이란?
    - memory에 올라가 있는 program의 수를 뜻한다
  - memory에 올라간 program이 몇개인지를 조절하는 역할을 장기 스케줄러가 담당한다
- Time sharing system에는 보통 장기 스케줄러가 없음 (무조건 ready status)

### Short-Term Scheduler (CPU scheduler)

> CPU scheduling을 하는 역할
>
- 어떤 process를 다음번에 running 시킬지 결정
- process에 `CPU` 를 주는 문제
- 충분히 빨라야 함 (millisecond 단위)

### Medium-Term Scheduler (Swapper)

> Time sharing system은 장기 스케줄러를 두지 않고 중기 스케줄러를 둔다
>
- 여유 공간 마련을 위해 process를 통째로 memory에서 disk로 쫓아냄
- process에게서 `memory` 를 뺏는 문제

  → 일단 다 주고, memory가 부족해서 전체 시스템 성능이 떨어지면 memory에서 쫓아낸다

- `Degree of Multi-programming` 을 제어

## Process의 상태

### Suspended (stopped)

- 외부적인 이유로 process의 수행이 정지된 상태
- process는 통째로 disk에 `swap out` 된다
- ex)
  - 사용자가 프로그램을 일시 정지시킨 경우 (by break key)
  - system이 여러 이유로 process를 잠시 중단시킨 경우

      (memory에 너무 많은 process가 올라와 있을 때)

      → 중기 스케줄러가 여유 공간 마련을 위해 process를 통째로 memory에서 disk로 쫓아낸다

### Blocked vs Suspended

- Blocked
  - 자신이 요청한 event가 만족되면 Ready
- Suspended
  - 외부에서 resume 해 주어야 Active

## Process 상태도

> Suspended를 포함한 상태도
>

<p align="center" width="100%">
  <img width="754" alt="process status" src="https://github.com/chloe-codes1/TIL/assets/53922851/3ed6f386-fd98-40e5-b692-6013748dc4e9">
</p>

### Suspended Blocked

- I/O 작업을 하다가 suspended 로 들어가면,
  - I/O 작업은 그대로 진행하고 Suspended Blocked 로 들어간다
  - I/O 작업이 끝나면 Suspended Ready로 간다
    - 오래 걸리는 작업이 끝나면 Blocked → Ready로 가는 것 처럼 Suspended Blocked → Suspended Ready로 간다

### Swap Out / Swap In

- Swap out
  - memory에서 통째로 쫓겨나는 것
- Swap in
  - 다시 memory에 올라가는 것

### Running (User mode / Monitor mode)

<p align="center" width="100%">
  <img width="753" alt="running status" src="https://github.com/chloe-codes1/TIL/assets/53922851/2ac2c638-823d-4ff1-9b5d-6c634e96c554">
</p>

- `Running (User mode)`
  - process에서 자기 code를 실행할 때
- `Running (Monitor mode)`
  - OS에 system call을 해서 OS의 code가 실행중일 때
  - 해당 program은 CPU를 빼앗긴게 아니므로 CPU를 사용중인 것으로 간주한다
    - System call을 호출한 경우
      - process가 kernel mode에서 running이다
    - Interrupt를 받은 경우
      - e.g. CPU running 중 I/O controller가 다른 interrupt를 발생시켜 OS에 CPU가 넘어가는 경우
      - 해당 program과 관련 없는 이유로 interrupt 를 받았음에도, Running 중인 것으로 간주한다

          → OS 가 Running 중이라고는 표현하지 않는다

          → Interrupt 받기 전 process가 Running 중인 것으로 간주한다

## Thread

> *“A `thread` (or `lightweight process`) is basic unit of CPU utilization”*
→ CPU 실행의 단위이다
>
- Process에서 CPU 수행에 실행에 필요한 부분만 별도로 가지고 있는 것이 Thread이다
- Process는 공유하고, Thread는 작업에 따라 각자 갖는다

<p align="center" width="100%">
  <img width="956" alt="thread address space" src="https://github.com/chloe-codes1/TIL/assets/53922851/2774cb24-80b7-4b65-8cc0-fd9ef2e97c8e">
</p>

### Thread의 구성

<p align="center" width="100%">
 <img width="959" alt="component of thread" src="https://github.com/chloe-codes1/TIL/assets/53922851/779cb0da-ea79-48e8-8200-ef21d04ddc69">
</p>

- program counter
- register set
- stack space
  - 주소 공간에서는 thread가 함수 호출과 관련된 stack 만을 갖는다
  - 그 외에는 process 내에서 다른 thread들과 공유한다

### Thread가 동료 thread와 공유하는 부분 (= `task`)

- code section
- data section
- OS resources

→ 전통적인 개념의 heavyweight process는 하나의 thread를 가지고 있는 task로 볼 수 있다

### Thread의 장점

- `Responsiveness`
  - 다중 thread로 구성된 task 구조에서는, 하나의 server thread가 blocked (waiting) 상태인 동안에도 동일한 task 내의 다른 thread가 실행(running) 되어 `빠른 처리`를 할 수 있다
- `Resource Sharing`
  - 여러개의 thread는 process의 binary code, data, resource를 공유할 수 있다
- `Economy`
  - creating & CPU switching thread (rather than a process)
  - solaris의 경우, 위 두 가지 overhead가 각각 30배, 5배이다
- `Throughput & Performance`
  - 동일한 일을 수행하는 다중 thread가 협력하여 `높은 처리율(throughput)`과 `성능 향상`을 얻을 수 있다
- `Utilization of Multi-Programming Architectures`
  - thread를 사용하면 `병렬성`을 높일 수 있다

### Implementation of Threads

- `Kernel Threads`

    > supported by kernel
    >
  - OS가 thread의 존재를 알고 있는 경우
  - OS가 서로 다른 thread 간의 CPU를 넘기는 작업을 할 수 있다 (like proces)
- `User Threads`

    > supported by library
    >
  - OS가 thread의 존재를 모르는 경우
    - OS가 보기에는 thread가 없는 하나의 process로 보이는 경우
  - OS가 thread 간의 CPU를 넘기는 작업을 할 수 없다
    - process 내부에서 OS에 비동기식 I/O를 요청해서 바로 다시 받아 다른 thread로 CPU를 넘기는 등 사용자 프로그램단에서 관리하는 것을 의미한다

## Process Creation

- Parent process가 child process를 생성
  - parent process와 똑같은 process를 복제하여 child를 생성한다
  - 직접 만들지는 못하고, system call을 통해 OS에 만들어 달라고 요청해서 child 를 생성한다

      → fork()

- process의 tree (계층 구조) 형성
- process는 자원을 필요로 한다
  - OS로부터 받는다
  - parent process와 공유할 수 있다
    - but, 사실은 parent와 child process는 별개의 process이므로 자원을 할당받기 위해 `경쟁` 한다
- 자원의 공유
  - parent와 child가 모든 자원을 공유하는 모델
  - 일부를 공유하는 모델
  - 전혀 공유하지 않는 모델
- Execution
  - parent와 child는 공존하며 수행되는 모델
  - child가 terminate 될 때 까지 parent가 기다리는 모델
- Address space
  - child는 parent의 공간을 복사한다 (binary & OS data)
  - child는 그 공간에 새로운 프로그램을 올린다
- Unix의 예
  - `fork()` system call이 새로운 process를 생성
    - parent를 그대로 복사 (OS data except for PID + binary)
    - 주소 공간 할당
  - fork 다음에 이어지는 `exec()` system call을 통해 새로운 프로그램을 메모리에 올린다

## Process Termination

- process가 마지막 명령을 수행한 후 OS에게 이를 알려줌 → `exit`
  - child가 parent에게 output data를 보낸다 (via `wait`)
  - process의 각종 자원들이 OS에게 반납된다
- parent process가 child 의 수행을 종료시킴 → `abort`
  - child가 할당된 자원의 한계치를 넘어섬
  - child에게 할당된 task가 더 이상 필요하지 않음
  - parent가 exit 하는 경우
    - OS는 parent process가 종료하는 경우, child가 더 이상 수행되도록 두지 않는다
    - tree 에서 가장 하위부터 단계적으로 종료한다

## fork() system call

- Process는 fork() system call에 의해 생성된다
  - caller를 복제해 새로운 address space를 생성한다

### Parent process와 Child process 구분

<p align="center" width="100%">
 <img width="938" alt="parent process and child process" src="https://github.com/chloe-codes1/TIL/assets/53922851/6e44b7db-213b-46b3-95c3-cb9103b1b79d">
</p>

- fork() 를 수행했을 때, parent process는 child process의 pid를 return 값으로 받게 된다
  - child process는 0을 반환한다

## exec() system call

- process는 exec() system call에 의해 서로 다른 여러개의 program을 실행할 수 있다
- caller의 memory image를 새로운 program으로 바꾼다
- 하나의 process 를 완전히 새로운 process로 덮어 씌워서 실행한다

<p align="center" width="100%">
 <img width="932" alt="exec() system call" src="https://github.com/chloe-codes1/TIL/assets/53922851/53618845-c495-4da2-854b-9c2509a1e715">
</p>

- execlp()
  - 해당 함수 내에서 exec system call을 호출한다
  - parameter
    - 1st: program 이름
    - 2nd: program에 전달할 argument

### fork() 와 exec()

child process를 생성하여 다른 program을 돌리고 싶을 때,

- fork()를 실행하여 복제한 후
- child process에는 exec()을 실행하여
  - parent process는 원래 실행하던 program을 이어서 실행하고
  - child는 새로운 program을 실행할 수 있게 한다

## wait() system call

- Process A 가 wait() system call을 호출하면,
  - kernel은 child가 종료될 때 까지 process A를 sleep 시킨다 → `block 상태`
    - 오래 걸리는 작업을 기다리도록 하는 blocked 외에, 공유 되는 자원에 대해 자식 process
  - child process 가 종료되면, kernel은 process A 를 깨운다 → `ready 상태`

<p align="center" width="100%">
  <img width="951" alt="wait() system call" src="https://github.com/chloe-codes1/TIL/assets/53922851/08767a9b-eba3-4d6c-8f1a-7428f3acc143">
</p>

- linux에서 command를 입력할 때, 입력 받는 한 줄이 하나의 process 다
  - shell process 가 하나 떠있는 것!
- command 를 실행하면, 해당 command의 자식 process 형태로 실행된다
  - 부모 process는 blocked status이므로, sleep 상태가 된다
    - ex) vi 명령어로 editor를 열었을 때 terminal이 block 상태가 되는 것
  - 부모 process는 자식 process가 종료될 때 까지 wait 상태가 된다

<p align="center" width="100%">
 <img width="667" alt="parent & child process" src="https://github.com/chloe-codes1/TIL/assets/53922851/e9b14d76-a744-4a10-bf41-5bdfdf2b350c">
</p>

## exit() system call

### Process의 종료

- `자발적 종료`
  - 마지막 statement 수행 후 exit() system call을 통해서 종료
  - program에 명시적으로 적어주지 않아도 main 함수가 return되는 위치에 compiler가 넣어줌
- `비자발적 종료`
  - 부모 process가 자식 process를 강제 종료시킴
    - 자식 process가 한계치를 넘어서는 자원 요청
    - 자식에게 할당된 task가 더 이상 필요하지 않음
  - 키보드로 kill, break 등을 친 경우 → interrupt
  - 부모가 종료하는 경우
    - 부모 process가 종료하기 전에 자식들이 먼저 종료됨

## Process 와 관련한 system call

- fork()
  - create a child (copy)
- exec()
  - overlay new image
- wait()
  - sleep util child is done
- exit()
  - frees all the resources, notify parent

## Process 간 협력

### Independent Process

process는 각자의 주소 공간을 가지고 수행되므로, 원칙적으로 하나의 process 는 다른 process의 수행에 영향을 미치지 못함

→ 독립적이다!

### Cooperating Process

Process 협력 메커니즘을 통해 하나의 process가 다른 process의 수행에 영향을 미칠 수 있음

### IPC: Interprocess Communication

<p align="center" width="100%">
 <img width="953" alt="message passing vs shared memory" src="https://github.com/chloe-codes1/TIL/assets/53922851/9b8b479e-ece9-418d-8f13-6018f15482b5">
</p>

- `message passing`
  - 설명
    - 메시지를 전달하는 방법
    - kernel을 통해 메시지를 전달한다
  - `Message System`
    - process 사이에 shared variable을 일체 사용하지 않고 통신하는 system
  - `Direct Communication`
    - 통신하려는 process의 이름을 명시적으로 표시
    - 메시지를 누구한테 보낼지를 명시하여 양자간에 합의된 명시적 메시지 전달 방식
  - `Indirect Communication`
    - mailbox (or port)를 통해 메시지를 간접 전달
    - 타겟을 명시하지 않고 전달하면, 협력하는 process 중 하나가 꺼내가도록 하는 방식
- `shared memory`
  - 주소 공간을 공유하는 방법
  - 서로 다른 process 간에도 일부 주소 공간을 공유하게 하는 shared memory 메커니즘이 있음
  - 단, 서로 신뢰할 수 있을 때만 공유해야 함
- 참고) `thread`
  - thread는 사실상 하나의 process 이므로 process 간 협력으로 보기는 어렵지만, 동일한 process를 구성하는 thread들 간에는 `주소 공간을 공유`하므로 협력이 가능하다
