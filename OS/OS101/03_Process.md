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
