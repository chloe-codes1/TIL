# JVM

<br/>

### JVM의 역할

- Java application을 class loader를 통해 읽어들여 Java API와 함께 실행한다
- JVM은 Java와 OS 사이에서 `중재자 역할`을 수행한다
  - Java가 OS에 구애받지 않고, `재사용`을 가능하게 해준다
- 가장 중요한 메모리 관리, `Garbage Collection`을 수행한다

### Java 프로그램 실행 과정

- 프로그램이 실행되면 JVM은 OS로 부터 프로그램이 필요로하는 `메모리를 할당` 받는다
  - JVM은 이 메모리를 용도에 따라 여러 영역으로 나누어 관리한다
- `Java 컴파일러 (javac)`가 자바 소스코드 (.java)를 읽어들여 자바 바이트 코드 (.class)로 변환한다
- `Class loader`를 통해 class 파일들을 JVM으로 로딩한다
- 로딩된 Class 파일들은 `Execution engine`을 통해 해석된다
- 해석된 바이트코드는 `Runtime Data Areas`에 배치되어 실질적인 수행이 이루어진다
  - `Runtime Data Areas`: 프로그램을 실행하기 위해 OS에서 할당받은 메모리 공간

이 과정 속에서 JVM은 필요에 따라 Thread Synchronization과 GC같은 관리 작업을 수행한다
