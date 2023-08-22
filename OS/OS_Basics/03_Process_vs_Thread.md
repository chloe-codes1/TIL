# Process vs Thread

<br>

- `Process`란 간단히 말해서 실행 중인 프로그램이다
  - 프로그램을 실행하면, OS로부터 실행에 필요한 자원 (memory)를 할당받아 `process`가 된다
  - 즉, `process`는 실행중인 프로그램으로 Disk로부터 memory에 적재되어, CPU의 할당을 받을 수 있는 것을 말한다.
- `Process`는 프로그램을 수행하는데 필요한 주소 공간, file, memory 등의 자원, 그리고 `thread`로 구성되어 있으며,
  - `Process`의 자원을 이용해서 실제로 작업을 수행하는 것이 바로 `thread`이다
- `Process`는 함수의 매개변수, 복귀 주소, 로컬 변수와 같은 임시 자료를 갖는 **프로세스 스택**과 전역 변수를 수록하는 **데이터 섹션**을 포함한다
  - 또한, `process`는 실행 중에 **동적으로 할당되는 메모리**인 **Heap**을 포함한다
- 모든 `process`에는 최소한 하나 이상의 `thread`가 존재하며, 둘 이상의 `thread`를 가진 `process`를 **multi-threaded process**라고 한다
  - Tip) Thread를 process라는 작업 공간 (공장)에서 작업을 처리하는 일꾼 (worker)로 생각하면 이해하기 쉽다!
- 하나의 `process`가 가질 수 있는 `thread`의 개수는 제한되어 있지 않으나, `thread`가 작업을 수행하는데 개별적인 메모리 공간 (`호출 스택`)을 필요로 하기 때문에 `process`의 memory 한계에 따라 생성할 수 있는 `thread`의 수가 결정된다
