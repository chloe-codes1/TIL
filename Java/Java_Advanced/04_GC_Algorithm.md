# Garbage Collection Algorithm

<br>

### Parallel CG

> Java 8에서 default GC로 적용
>

- minor collection을 `병렬` 로 수행한다
  - GC의 오버헤드를 현저하게 줄일 수 있다
- multi processor나 multi thread hardware 에서 돌아가는 `중대형 규모의 데이터셋` 을 다루는 어플리케이션을 위한 GC
- `Parallel Compaction`
  - Parallel Collector가 major collection을 `병렬` 로 수행하게 해주는 기능
  - `-XX:+UseParallelGC` 옵션을 지정하면 Parallel Compaction이 디폴트로 사용된다
- but, multi thread를 사용한 collection 사용이 `Young` 영역에 국한된다
  - Young Generation Collection 알고리즘: `Parallel Scavenge`
  - Old Generation Collection 알고리즘: `Serial Mark-Sweep-Compact`

<br>

### G1 (Garbage First Collector)

> Java 11에서 default GC로 적용
>

- 큰 메모리를 가진 멀티 프로세서 머신을 위한 Collector
- `-XX:+UseG1GC` 옵션으로 G1 Collector를 켤 수 있다
- G1 GC만 Generational GC가 아니라는 점에 주의해야한다
  - G1 collector는 Young 영역과 Old 영역으로 나누지 않는 방식을 사용하는 특이한 collector이다
  - G1은 물리적 generation 구분을 없애고, 전체 heap을 1MB 단위의 region들로 다룬다
    - `바둑판 모양`으로 구성되어 있으며, `약 2000개`의 구역을 사용한다
  - G1 이라는 이름은 garbage로 가득찬 region부터 컬렉션을 시작한다는 의미이다
    - Garbage로 꽉 찬 region이 발견되면 바로 collector를 돌린다.
- Old region의 살아있는 객체는 다른 Old region으로 옮겨지며, compaction이 이뤄진다
- G1에서 Young, Old 영역 개념은 `고정된 개념`이 아니다
  - 객체가 `새로 할당`되는 region들의 집합이 `Young` generation 이다
  - `프로모션`이 일어나는 region의 집합이 `Old` Generation 이다

<br>

### ZGC

> Java 17에서 default GC로 적용
>

ZGC는 8MB에서 16TB 크기의 heap을 처리할 수 있는 확장 가능한 low-latency GC이며 `-XX:+UseZGC` option을 사용하여 활성화 할 수 있다

- `Low-latency`
  - ZGC는 memory collection을 위해 일시 중단을 최소화하여 응답성을 높인다
  - collection 작업을 수행하는 동안 application thread는 계속 실행되는 concurrent GC이며, 중단 시간은 매우 짧다
    - 이로 인해 대규모 memory 환경에서도 높은 응답성을 유지할 수 있다
    - 최대 지연 시간은 1밀리초 미만이다
- `매우 큰 Heap 지원`
  - ZGC는 수 16TB에 달하는 큰 heap을 처리할 수 있다
    - 이로 인해 대규모 데이터 처리나 memory 집약적인 작업을 수행하는 application에 사용하기 좋다
- `불연속적인 수집`
  - ZGC는 전체 heap을 한 번에 수집하는 대신, 작은 region 단위로 분할하여 garbage collection을 수행한다
  - 수집 작업의 일부만을 처리하므로 일시 중단 시간을 분산시킬 수 있다
- `병렬 처리`
  - ZGC는 multi-thread를 활용하여 GC 작업을 병렬로 처리한다
  - 이를 통해 GC 작업을 효율적으로 분산시키고, 전체 collection 시간을 단축한다
- `효율성`
  - collection 중에 힙을 정리할 필요가 없기 때문에 효율적이다
    - 일반적인 GC는 memory collection 작업을 수행하기 위해 `stop-the-world` 를 발생시킨다
      - 이때, application thread들이 모두 일시 중단되어 GC 작업이 이루어진다
      - 이러한 중지 시간은 application 응답성과 성능에 영향을 줄 수 있다
    - 반면 ZGC는 heap을 정리하는 과정에서 중지 시간을 매우 짧게 유지한다
  - ZGC는 collection 작업 중에도 application thread를 계속 실행시키며, 필요한 경우에만 매우 짧은 중지 시간을 발생시킨다
    - ZGC는 일시 중단 시간을 최소화하여 application 응답성을 높이는데 중점을 준다
