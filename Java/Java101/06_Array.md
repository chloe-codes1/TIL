# Java Array

<br>

<br>

## Array (배열)

- 같은 타입의 여러 변수를 하나의 묶음으로 다루는 것

- 배열은 같은 타입의 기억공간을 하나의 이름으로 모아서 handling 할 수 있는 자료형이다.

- 위치 첨자가 따라다니는 변수 

  => 위치 인덱스가 반드시 따라다님

  <br>

### 1. 선언   

  타입[] 변수이름;  

ex) 

```java
// ver1) 
int[] scores;

// ver2)
int scores[];   
```

<br>

### 2. 생성   

  변수이름 = new 타입[길이];

ex) 

```java
int [] nums = new int [5];
```

 -> 배열의 선언과 생성을 한번에 했음

  \* *배열의 길이는 int범위의 양의 정수(0도 포함) 이어야 한다!*

<br>

\3. 초기화

   : 배열은 생성과 동시에 자동적으로 자신의 타입에 해당하는 기본값으로 초기화되므로 사용하기 전에 따로 초기화를 해주지 않아도 되지만, 원하는 값을 저장하려면 각 요소마다 값을 지정해줘야함





Int num;   -> Stack영역에 num이라는 기억공간 만들어줘

=> 그리고 여기엔 정수가 들어갈꺼야



Int [] nums =new int[5] ; 

=> 배열 선언한 순간 참조형 (reference type)이 된다!!!

-> stack영역에 nums라는 주소 만들어줘

-> new니까 Heap 영역에 int type으로 방 5개 만들어   => heap이니까 JVM이 관리

  => 그러면 JVM에 의해 5개방에 각각 int 니까 0으로 default 초기화가 일어남

 -> 한번 이렇게 만들면 resizing 안됨

 -> 연속적인 공간을 할당 받는다는 보장을 받음 

-> 배열 또한 Class이므로 method 쓸 수 있다



Int [] nums.length ;  -> nums라는 배열의 사이즈 어떻게 되니?





String name;  -> Stack영역에 String이라는 기억 공간 만들어줘

   => 그리고 여기엔 주소가 들어갈꺼야



String[] names = new String[5];

=> reference type!

  => JVM에 의해 5개 방이 각각 null으로 default초기화 일어남

  => 주소가 들어 갈 것 이라서 . 가 들어감



Names[0] = “홍길동”;

  => names의 0번째 방에 코드표 영역의 “홍길동”을 가리키는 주소가 저장됨





Oracle에서 args 실행하기

![img](https://lh3.googleusercontent.com/uGqQh0xF6AbgCvfISK3_liROQRWTzf6W_F__F1W-tJnGakIAnExSAP-kiAUABWS66CIzSviOy-k6xPS-z9tXuM9kNFFn1hZ70fO3kdcDrb7NV2hxCHg_XSs6qBczN-yfYJhZsKZQ)