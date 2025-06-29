# Variables in Java

<br>

### 1. Member variable (Instance variable)

> Declared in a class, but outside a method

```
Class A {

 String name; 

}                  
```

- `Class`의 일원

- Class 안에서 선언된 변수

- `Instance`가 생성될 때 생성됨

- Instance 변수의 값을 읽어오거나, 저장하려면 Instance를 먼저 생성해야 함!

- 초기값을 설정하지 않으면 자동 default 초기화가 됨  

  ex) String name = null;  할 필요 없음!
  
  

<br>

### 2. Local variable

```
Public Static Void main(~~~) {  

	String name;

}
```

- 함수의 일원

- method(함수) 안에서 선언된 변수

  - method 내에서만 사용 가능

- method가 실행 될 때 memory를 할당 받으며, 끝나면 소멸되어 사용할 수 없다

- default 초기화가 안됨  

  ex) String name = null; 해줘야 함

<br>

### 3. Class variable (Static variable)

> Declared with the `static keyword` in a class, but outside a method, constructor, or block

- Instance variable에 `static`만 붙이면 됨
- 인스턴스 변수는 각각 고유한 값을 가지지만, 클래스 변수는 모든 인스턴스가 공통된 값을 공유하게 됨
  - 한 클래스의 모든 인스턴스들이 공통적인 값을 가져야할 때 클래스 변수로 선언한다!
- 클래스가 로딩될 때 생성되어(= **메모리에 딱 한번만 올라감**) 종료 될 때 까지 유지된다
- `public` 을 붙이면 같은 프로그램 내에서 어디서든 접근할 수 있는 **전역 변수**가 됨
- 인스턴스 변수의 접근법과 다르게 인스턴스를 생성하지 않고 클래스이름 & 클래스변수명을 통해서 접근



<br><br>

### `Null Assign`을 하는 이유 (from docs.oracle)

: **Assign null to Variables That Are No Longer Needed**

Explicitly assigning a null value to variables that are no longer needed helps the garbage collector to identify the parts of memory that can be safely reclaimed. Although Java provides memory management, it does not prevent memory leaks or using excessive amounts of memory.

An application may induce memory leaks by not releasing object references. Doing so prevents the Java garbage collector from reclaiming those objects, and results in increasing amounts of memory being used. Explicitly nullifying references to variables after their use allows the garbage collector to reclaim memory.

One way to detect memory leaks is to employ profiling tools and take memory snapshots after each transaction. A leak-free application in steady state will show a steady active heap memory after garbage collections.

<br>

<br>

*다 쓰고 난 자원은 null assign을 해야한다!*

-> null assign을 하지 않으면 자원을 많이 먹어서 성능이 안좋아지기 때문!

<br>

 But, null assign 한다고 모든 자원이 반납되는게 아니다

```
input.close();

Input = null;
```

  -> 이렇게 해야 다 반납 할 수 있음
