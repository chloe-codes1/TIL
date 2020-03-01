# Variables in Java

<br>

### 1. Member variable

```
Class A {

 String name; 

}                  
```

- Class의 일원

- class 안에서 선언된 변수

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

- default 초기화가 안됨  

  ex) String name = null; 해줘야 함



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