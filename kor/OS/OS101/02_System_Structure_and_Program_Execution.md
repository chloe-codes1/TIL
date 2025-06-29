# System Structure & Program Execution

> Reference: [이화여대 운영체제 강의 - 반효경 교수님](http://www.kocw.net/home/cview.do?cid=4b9cd4c7178db077)
>

<br>

## 컴퓨터 시스템 구조

### Mode bit

- Mode bit이란?
  - 사용자 프로그램의 잘못된 수행으로 다른 프로그램 및 운영체제에 피해가 가지 않도록 하기 위한 보호 장치
- Mode bit이 필요한 이유
  - CPU가 사용자 프로그램에 넘어가면 운영체제는 제어할 수 없기 때문
  - CPU에서 기계어를 실행할 때 운영체제가 실행하는지 or 사용자 프로그램이 실행하는지 구분하는 존재가 필요하다
- Mode bit의 종류

    > Mode bit을 통해 하드웨어적으로 두 가지 모드의 operation을 지원한다
    >
  - `1 사용자 모드`
    - 사용자 프로그램 수행
    - 위험한 기계어 (특권 명령)는 사용할 수 없게 제한한다
  - `0 모니터 모드 (= Kernel mode, System mode)`
    - OS 코드 수행
    - 보안을 해칠 수 있는 중요한 명령어 (`특권 명령`)는 모니터 모드에서만 수행 가능하다
- Mode bit 전환 방식
  1. Interrupt나 exception 발생 시 하드웨어가 mode bit을 0으로 바꾼다
     - Interrupt는 CPU Interrupt를 뜻함
       - from Disk controller, I/O controller, etc.
     - exception은 권한이 없는 작업을 실행하려고 할 때 발생하는 exception을 뜻함

  2. 사용자 프로그램에게 CPU를 넘기기 전에 mode bit을 1로 세팅한다

### Registers

- Register란?
  - 연산의 output을 저장하기 위한 용도로, CPU에 붙어있다
- Register의 종류
  - PC (Program Counter) Register
    - 다음번에 실행할 기계어의 memory 주소를 가지고 있다

            == 주소를 가리키고 있다

    - CPU는 PC register가 가리키고 있는 memory 주소의 기계어를 실행한다

            → 실행이 끝나면 그 다음 위치의 기계어를 실행한다

    - CPU Interrupt가 발생하면 PC Register가 바라보고 있는 memory는 OS가 된다

### Timer

- Timer란?
  - CPU 사용권을 뺏어오는 작업은 OS가 할 수 없음

        → CPU의 `독점`을 막기 위한 `hardware`가 필요하고, 그게 바로 Timer다

- Timer의 역할
  - 정해진 시간이 흐른 뒤 OS에게 제어권이 넘어가도록 Interrupt를 발생시킨다
    - 일정 시간이 지나면 Interrupt 를 발생시켜서 CPU의 사용권을 뺏어오는 역할을 한다
- Timer 동작 방식
  - Timer는 매 clock tick 마다 1씩 감소한다
  - Timer 값이 0이 되면 Timer Interrupt가 발생한다
  - CPU를 특정 프로그램이 독점하는 것으로 부터 보호한다

## Interrupt

- Interrupt 동작 방식
  - Interrupt 당한 시점의 register와 Program Counter를 저장한 후 CPU의 제어를 Interrupt 처리 루틴에 넘긴다
- Interrupt 의 의미
  - `Interrupt (Hardware Interrupt)`
    - Hardware가 발생시킨 Interrupt
    - ex) I/O Controller가 일으킨 Interrupt
  - `Trap (Software Interrupt)`
    - `Exception`
      - Program이 오류를 범한 경우
      - Program이 특권 명령을 수행하려고 하면 발생
    - `System Call`
      - Program이 Kernel 함수를 호출하는 경우
- Interrupt 관련 용어
  - Interrupt Vector
    - 해당 Interrupt 처리 루틴 주소를 가지고 있음
  - Interrupt 처리 루틴

        (= Interrupt Service Routine, Interrupt Handler)

    - 해당 Interrupt를 처리하는 Kernel 함수

## System Call

- System Call이란?
  - 사용자 프로그램이 OS의 서비스를 받기 위해 Kernel 함수를 호출하는 것
  - CPU가 I/O 를 요청하는 기계어는 `특권 명령`이다
    - 즉, 사용자 프로그램이 실행할 수 없다

            (mode bit이 1인 사용자 모드일 때는 특권 명령을 수행할 수 없기 때문)

    - 그래서 OS에 해달라고 요청을 해야한다

            → 그게 바로 System Call 이다

  - 사용자 프로그램이 스스로 Interrupt를 거는 것을 System Call 이라고 한다
    - CPU를 OS에 넘기기 위해서 직접 Program Counter를 넘길 수 없기 때문에 Interrupt를 건다

## Device Controller

- I/O Device Controller
  - 해당 I/O 장치 유형을 관리하는 일종의 작은 CPU
  - 제어 정보를 위해 `control register` , `status register` 를 가짐
    - `control register`
      - processor나 다른 hardware 장치의 동작을 제어하고 구성하기 위해 사용되는 register
    - `status register`
      - processor의 현재 상태와 flag 정보를 저장하는 register
      - 주로 processor의 실행 상태, 연산 결과, Interrupt 상태와 관련된 정보를 저장하고 제어한다
      - Flag 종류
        1. Zero Flag (ZF)
            1. 연산 결과가 0인 경우에 설정된다
            2. 주로 비교 연산과 관련되어 사용된다
        2. Sign Flag (SF)
            1. 연산 결과가 음수인 경우에 설정된다
        3. Overflow Flag (OF)
            1. 연산 결과가 오버플로우가 발생한 경우에 설정된다
            2. 정수 연산에서 사용된다
        4. Carry Flag (CF)
            1. 연산 결과가 캐리(자리 올림)가 발생한 경우에 설정된다
            2. 산술 연산에서 사용된다
        5. Parity Flag (PF)
            1. 연산 결과의 하위 비트들 중 1의 개수가 짝수일 경우에 설정된다
  - local buffer를 가짐 (일종의 data register)
- I/O 는 실제 device 와 local buffer 사이에서 일어남
- Device Controller는 I/O 가 끝났을 경우 Interrupt 로 CPU에게 그 사실을 알림
- 용어 정리
  - Device Driver (장치 구동기)
    - OS 코드 중 각 장치별 처리 루틴 → software
    - CPU가 device controller에게 부탁을 하는 기계어
    - 컴퓨터 내부에서 CPU가 수행하는 코드
  - Device Controller (장치 제어기)
    - 각 장치를 제어하는 일종의 작은 CPU  → hardware

## CPU가 OS에 넘어가는 경우

> Interrupt가 걸리면 넘어간다
>
1. Hardware 장치들이 Interrupt를 거는 경우

    → 진정한 의미의 Interrupt

    - Timer
        - CPU의 독점을 막기위한 hardware
2. Program이 직접 Interrupt line을 설정하는 경우
    - System call
        - CPU가 I/O 를 요청하는 기계어는 `특권 명령` 이라 사용자 Program이 실행할 수 없기 때문에 존재한다

## Sync I/O vs Async I/O

> 두 경우 모두 I/O 완료는 Interrupt를 통해 알려준다
>

- `동기식 입출력 (Synchronous I/O)`
  - I/O 요청 후 입출력 작업이 `완료된 후`에야 제어가 사용자 프로그램에 넘어감
  - 구현 방법
        1. I/O가 끝날 때가지 CPU를 낭비시킴
            - 매 시점 하나의 I/O만 일어날 수 있음
        2. I/O가 완료될 때까지 해당 프로그램에게서 CPU를 빼앗고, I/O 처리를 기다리는 줄에 그 프로그램을 줄 세움
            - 다른 프로그램에게 CPU를 줌
- `비동기식 입출력 (Asynchronous I/O)`
  - I/O 가 시작된 후 입출력 작업이 끝나기를 `기다리지 않고` 제어가 사용자 프로그램에 `즉시` 넘어감

## DMA (Direct Memory Access)

- 빠른 I/O 장치를 memory에 가까운 속도로 처리하기 때문에 사용

    → memory에 직접 접근하기위한 장치

- CPU의 중재 없이 device controller가 device의 buffer storage의 내용을 block 단위로 직접 전송
- Byte 단위가 아니라 block 단위로 interrupt를 발생시킨다
