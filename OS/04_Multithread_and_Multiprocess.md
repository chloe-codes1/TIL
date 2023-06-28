# Multithread and Multiprocess

<br>

## Multithreading

### Multithreading의 장점

- Process를 이용하여 동시에 처리하던 일을 thread로 구현할 경우, memory 공간과 system 자원 소모가 줄어들게 된다
- Thread 간의 통신이 필요한 경우에도 별도의 자원을 이용하는 것이 아니라, 전역 변수의 공간 또는 동적으로 할당된 공간인 `Heap 영역`을 이용하여 데이터를 주고받을 수 있다
  - 그렇기 때문에  process 간 통신 방법에 비해 thread간 통신 방법이 훨씬 간단하다
- Thread의 `context switch` 는 process의 `context switch`와는 달리 캐시 메모리를 비울 필요가 없기 때문에 더 빠르다
  - 따라서 시스템의 throughput (처리량)이 향상되고,
  - 자원 소모가 줄어들며,
  - 자연스럽게 프로그램의 응답시간이 단축된다
- 이러한 장점 때문에 작업들을 하나의 process에서 thread로 나눠 수행한다

<br>

### Multithreading의 문제점

- `Multi-process`를 기반으로 프로그래밍 할 때는 process 간에 공유하는 자원이 없기 때문에 동일한 자원에 동시에 접근할 일이 없지만, `multi-threading` 을 기반으로 프로그래밍을 할 때는 이 부분을 신경써줘야 한다
  - 서로 다른 thread가 data와 heap 영역을 공유하기 때문에 어떤 thread가 다른 thread에서 사용중인 변수나 자료구조에 접근하여 엉뚱한 값을 읽어오거나 수정할 수 있다
- 그래서 `multi-threading` 환경에서는 `동기화 작업` 이 필요하다
  - 동기화를 통해 작업 처리 순서를 컨트롤하고, 공유 자원에 대한 접근을 컨트롤하는 것이다.
    - but, 이로 인해 `병목 현상`이 발생하여 성능이 저하될 가능성이 높다
      - 그러므로 과도한 `락` 으로 인한 병목 현상을 줄여야 한다
- `multi-thread` 환경에서 여러 thread가 하나의 자원을 공유하려고 할 때 `Deadlock` 과 같은 문제 상황이 발생할 수 있다

<br>

## Multithread vs Multiprocess

- `Multi-thread`
  - 장점
    - 멀티 스레드는 멀티 프로세스보다 적은 공간을 차지하고 context switching이 빠르다는 장점이 있지만,
  - 단점
    - 오류로 인해 하나의 스레드가 종료되면 전체 스레드가 종료될 수 있다는 점과
    - `동기화 문제`를 갖고 있다
- `Multi-process`
  - 장점
    - 멀티 프로세스 방식은 하나의 프로세스가 죽더라도 다른 프로세스에는 영향을끼치지 않고 정상적으로 수행된다는 장점이 있지만,
  - 단점
    - 멀티 스레드보다 많은 메모리 공간과 CPU 시간을 차지한다는 단점이 존재한다
- 정리
  - Multi-thread와 multi-process는 동시에 여러 작업을 수행한다는 점에서 같지만,
    - 적용해야하는 시스템에 따라 적합/부적합이 구분된다
  - 따라서 대상 시스템의 특징에 따라 적합한 동작 방식을 선택하고 적용해야한다
