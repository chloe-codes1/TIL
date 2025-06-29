# What is an OS?

> Reference: [이화여대 운영체제 강의 - 반효경 교수님](http://www.kocw.net/home/cview.do?cid=4b9cd4c7178db077)
>

## 운영체제란?

- 사용자가 하드웨어를 몰라도 컴퓨터 시스템을 `편하게` 사용할 수 있는 `환경`을 제공한다
- 컴퓨터 시스템의 한정된 `자원` (CPU, Memory, I/O)를으로 최대한의 성능을 내도록 `효율적`으로 관리한다
  - ex)
    - 실행중인 프로그램들에게 짧은 시간씩 CPU를 번갈아 할당 (`round robin`)
    - 실행중인 프로그램들에 memory 공간을 적절히 분배
      - memory: CPU의 작업 공간
- 컴퓨터 하드웨어 바로 위에 설치되어 사용자 및 다른 모든 소프트웨어와 하드웨어를 연결하는 `소프트웨어 계층`
  - 좁은 의미 (커널)
    - 운영체제의 핵심 부분으로 메모리에 상주하는 부분
  - 넓은 의미
    - 커널 뿐만 아니라 각종 주변 system utility를 포함한 개념

## 운영체제의 기능

- 컴퓨터가 부팅이 된다

    == memory에 운영체제가 올라간다

- Kernel
  - 컴퓨터가 실행되면 memory에 상주한다
- CPU 관리
  - 매 클럭마다 memory에 있는 기계어를 읽어와 연산을 한다
  - CPU는 직접 I/O 장치에 접근할 수 없다
    - I/O들은 각자 동작을 담당하는 작은 CPU와 같은 `I/O 컨트롤러`가 있고, CPU는 컨트롤러에 요청햐여 I/O 장치에 필요한 작업을 실행하게 한다
  - CPU Scheduling
    - 운영체제의 가장 중요한 기능!
    - 운영체제 내부에 있는 기계어가 CPU에게 특정 프로그램을 실행하도록 명령, 즉 스케줄링 한다
    - 한정된 시간동안만 특정 프로그램이 CPU를 사용하도록 하고, 주어진 시간이 끝나면 CPU를 다른 프로그램에 넘긴다

      → 운영체제가 단독으로 진행할 수는 없고, 하드웨어의 도움을 받는다

- Memory 관리
  - 한정된 memory를 어떻게 쪼개어 쓸지
- 디스크 Scheduling
  - 디스크는 느리다!
  - CPU는 오래 걸리는 작업(ex. 디스크에서 파일 읽기)을 실행하는 중에 다른 작업으로 넘어가서 다른 작업을 실행한다
  - CPU 처럼 I/O 장치에도 `여러 요청`이 동시에 들어오는데, 어떤 순서로 효율적으로 처리할지 운영체제가 scheduling 하여 자원을 효율적으로 사용할 수 있게 한다
- Interrupt 와 Caching
  - 빠른 CPU와 느린 I/O 장치 간 속도차를 완충하기 위해 Interrupt 와 Caching를 활용한다
  - Caching
    - 중간 단계를 두는 것
    - 자주 조회되는 데이터를 memory에 caching
  - Interrupt
    - CPU는 I/O 컨트롤러에 일을 시키고 `기다리지 않고` 당장 실행할 수 있는 작업을 찾아 해당 작업을 실행한다
      - I/O 컨트롤러는 작업이 완료 됐음을 `Interrupt` 를 통해 CPU에게 알린다
        - CPU는 매 작업이 끝난 후 `Interrupt check` 를 해서 실행한 작업들이 끝났는지 확인한다
    - Interrupt가 들어오면 CPU는 운영체제에게 넘어가고, 종료된 작업이 다시 CPU가 실행할 수 있게 한다
    - Interrupt는 느린 장치(ex. 디스크 I/O)들이 작업이 완료되었음을 CPU에게 알리기 위한 장치이다

## 운영 체제의 목적

- 컴퓨터 시스템을 편리하게 사용할 수 있는 환경을 제공
- 컴퓨터 시스템의 자원을 효율적으로 관리
  - 컴퓨터의 두뇌는 CPU 가 아니라 OS다! (교수님 생각)
    - CPU는 계산을 잘하는 존재
    - Memory는 기억을 하는 존재
    - OS는 그들을 어떻게 사용할지 `판단` 하는 존재 (통치자)
      - ex) 프로그램마다 메모리를 적절히 나눠줘야 하는데, 그 때 OS가 결정을 한다

## 운영 체제의 분류

### 동시 작업 가능 여부

- 단일 작업 (single tasking)
  - 한 번에 하나의 작업만 처리
- `다중 작업 (multi tasking)`
  - 동시에 두 개 이상의 작업 처리
  - ex) 하나의 명령의 수행이 끝나기 전에 다른 명령이나 프로그램을 수행할 수 있다

### 사용자의 수

- 단일 사용자 (single user)
  - ex) MS-DOS, MS Windows
- `다중 사용자 (multi user)`
  - ex) Unix, Linux
  - 다중 사용자가 쓸 수 있게 보안 / 권한 문제에 대한 해결이 필요함

### 처리 방식

- 일괄 처리 (Batch processing)
  - 작업 요청의 일정량을 모아서 한꺼번에 처리
  - 작업이 완전히 종료될 때까지 기다려야함
  - ex) 초기 Punch Card 처리 시스템
- `시분할 (Time sharing)`
  - 여러 작업을 수행할 때 컴퓨터 처리 능력을 일정한 단위로 분할하여 사용
  - 일괄 처리 시스템에 비해 짧은 응답 시간을 가짐
  - Interactive 한 방식
  - 주어진 자원을 시간을 쪼개서 최대한 효율적으로 쓰는 방식
  - ex) Unix
- 실시간(Realtime OS)
  - 정해진 시간 안에 어떠한 일이 반드시 종료됨을 보장되어야 하는 실시간 시스템을 위한 OS
  - 실시간 시스템의 개념 확장
    - Hard realtime system
      - Deadline을 어기면 큰 문제가 발생
      - ex) 원자로 / 공장 제어, 미사일 제어, 반도체 장비, 로봇 제어
    - Soft realtime system
      - Best effort → 최대한 노력하지만 보장은 못한다
      - ex) 동영상 플레이어 재생 시 프레임이 찍히지 않으면 영상이 끊김

### 용어 정리

아래의 4개 용어들은 기본적으로 같은 의미이나, 조금씩 강조하는 바가 다르다

- Multi-tasking
- Multi-programming
  - memory에 여러 프로그램이 동시에 올라가 있음을 강조
- Time sharing
  - CPU의 시간을 분할하여 나누어 쓴다는 의미를 강조
- Multi-process

아래 용어는 아예 다른 의미이다

- Multi-processor
  - 하나의 컴퓨터에 CPU (processor)가 여러개 붙어있음을 의미
  - 고성능 컴퓨팅, Cloud 컴퓨팅에서 다루는 문제

## 운영 체제의 예시

### UNIX

- 코드의 대부분을 C 언어로 작성
  - 운영체제가 하드웨어적 요소를 제어하려면 Assembly 언어로 작성해야 하는데, 그게 어려워서 사람이 이해하기에 편한 C 언어를 만듦
  - 사람이 이해하기 편해짐
- 높은 이식성
  - C언어는 여러 아키텍처에서 호환이 되므로 높은 이식성을 갖는다
- 최소한의 Kernel 구조
- 복잡한 시스템에 맞게 확장 용이
- 소스 코드 공개
- 프로그램 개발에 용이
- 다양한 버전
  - System V, FreeBSD, SunOS, Solaris
  - Linux

        → 소스코드 공개되어있고, 이걸 기반으로 발전하고 잇음

### DOS (Disk Operating System)

- MS사에서 1981년 IBM-PC를 위해 개발
- 단일 사용자용 운영체제
- 메모리 관리 능력에 한계가 있음 (주 기억장치: 640KB)

### MS Windows

- MS사의 다중 작업용 GUI 기반 운영 체제
- Plug and Play
- 네트워크 환경 강화
- DOS용 응용 프로그램과 호환성 제공
- 풍부한 지원 소프트웨어

## 운영 체제의 구조

### 프로세스 관리

- 프로세스 생성과 삭제
- 자원 할당 및 반환
- 프로세스 간 협력

### 그 외

- 보호 시스템
- 네트워킹
- 명령어 해석기 (command line interpreter)

## 프로세스

- 프로세스란?
  - 실행중인 프로그램
- CPU Queue
  - CPU를 쓰고자 하는 프로그램들을 줄 세워둔다

## CPU Scheduling

여러 프로그램들이 CPU 사용을 하고자 CPU queue에서 기다릴 때, 어떤 순서로 queue에 있는 작업을 실행할지 정하는 것

→ 운영체제의 중요 역할 중 하나

### FCFS (First-Come First-Served)

- 설명
  - 요청이 들어온 순서대로 처리하는 방법

        → 형평성 좋음

- 문제점
  - 먼저 들어온 요청이 CPU를 오래 점유하면 그 뒤에 들어온 작업들의 average waiting time이 길어짐

        → 효율성 좋지 않음

### SJF (Shortest-Job-First)

- 설명
  - CPU 사용시간이 가장 짧은 process를 제일 먼저 스케줄
  - Minimum average waiting time을 보장

        → 효율성은 좋음

- 문제점
  - Starvation (기아 현상) 발생 가능

        → 형평성 문제

### Round Robin (RR)

- 현대에 가장 많이 사용하는 방법
- 각 process는 동일한 크기의 CPU 할당 시간을 갖는다
  - 할당 시간이 끝나면 Interrupt 가 발생하여 process는 CPU를 빼앗기고 CPU queue의 제일 뒤에 줄을 선다
- n개 process가 CPU queue에 있는 경우
  - 어떤 process도 `(n-1)*할당시간` 이상 기다리지 않는다
    - 전체 process n개 - 나 자신
- 장점
  - 짧은 작업은 주어진 할당 시간에 빠르게 작업을 완료하면 되고, 긴 작업은 할당 시간동안 끝마치지 못한 작업을 다시 차례가 됐을 때 이어서 처리하면 된다

        → 대기 시간이 process의 CPU 사용시간에 비례한다

## 메모리 관리

- Swap 영역
  - 실행중인 process의 당장 필요한 공간은 memory에 올라가지만, memory의 공간적 한계로 다 올리지 못한 부분이 swap 영역에 올라간다
  - 영속 가능한 디스크에 위치하지만, 전원이 나가면 더이상 쓸모 없는 데이터다
    - 이미 해당 process는 실행중이 아니기 때문에

- 메모리에서 어떤 것을 쫓아낼까?
  - 미래에 다시 사용될 가능성이 높은 페이지는 쫓아내지 말고, 가까운 미래에 사용될 가능성이 낮은 페이지를 쫓아내야 효율적으로 관리된다!
- `LRU (Least Recently Used)`
  - 가장 오래 전에 참조된 페이지 삭제
- `LFU (Least Frequently Used)`
  - 가장 적게 참조된 페이지 삭제

## 디스크 스케줄링

- 디스크의 접근 시간 중 가장 많은 시간을 차지하는게 디스크 헤드 이동 시간

    → 헤드 이동 거리를 줄일 수 있게 스케줄링을 해야한다
- Seek time을 줄여야 한다!

    → 그러기 위해 디스크 스케줄링이 필요하다

### FCFS (First-Come First-Served)

오래걸림 (비효율적)

### SSTF (Shortest Seek Time First)

- 이동거리가 짧아 효율적
- but, starvation 문제가 발생한다

### SCAN

- 현재 디스크 스케줄링 방식
- queue에 들어온 요청에 상관 없이 head는 이동한다
- 이동하면서 queue에 들어온 요청이 있으면 처리한다

    → 엘리베이터의 동작 방식과 유사!

## 저장장치 계층구조와 Caching

- CPU는 기계어를 실행할 때 Register에 있는 값들로 실행한다
- CPU와 memory 사이의 속도 차이를 극복하기 위해 Cache Memory를 둔다
- 현재는 Main Memory와 Magnetic Disk 사이에 `Flash memory`가 위치한다
- Primary
  - 휘발성
  - CPU가 직접 접근 가능하다 (executable)
- Secondary
  - 비휘발성
  - CPU가 직접 접근할 수 없어서, Primary에 올려서 실행한다
- 속도 차이를 극복 (완충) 하기 위해 layered architecture를 갖는다
  - 빠른 계층으로 복사를 해놓고, 복사본을 읽어가는 것이 바로 `Caching`이다!
- Caching
  - copying information into faster storage system
  - 누구를 쫓아낼 것인가!

## Flash Memory

### Flash Memory 란?

- 반도체 장치 (하드디스크: 마그네틱)
- NAND형 (storage), NOR 형 (embeded code 저장용)
  - 우리가 사용하는것 (저장장치 목적)은 모두 NAND 형!

### Flash Memory 특징

- Non-volatile
  - 전원이 나가도 데이터가 유지가 된다
- Low power consumption
  - 하드디스크에 비해 전력 소모가 적다
- Shock resistance
  - 물리적 충격에 강하다
- Small size
- Lightweight
- 쓰기 횟수 제약
  - 특정 횟수 이상 사용하면 더이상 쓰기를 할 수 없다
- 데이터가 시간이 흐름에 따라 변질될 수 있다
  - cell 안에 들어가있는 전하의 양으로 데이터를 읽는데, 전하가 시간이 흐름에 따라 cell에서 빠지게 된다
    - 나중에는 읽히지 않게 될 수 있다

### Flash Memory의 사용 형태

- 휴대폰, PDA 등 embeded system 구성용
- USB용 memory stick
- SD 카드
- 모바일 장치 뿐만 아니라 대용량 시스템에서 SSD (Solid State Drive) 란 이름으로 하드디스크 대체 시도
