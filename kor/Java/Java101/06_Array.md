# Array in Java

<br>

## Array 알아보기

### Array 란?

- 같은 타입의 여러 변수를 하나의 묶음으로 다루는 것

- 배열은 같은 타입의 기억공간을 하나의 이름으로 모아서 handling 할 수 있는 자료형이다.

- 위치 첨자가 따라다니는 변수

  => 위치 인덱스가 반드시 따라다님

- 배열 또한 Class이므로 method 쓸 수 있다
- 배열은 한번 size가 정해지면 resizing이 안된다!

<br>

### Array의 단점

- `크기`를 `변경할 수 없다`
  - 확장이 필요할 경우 새로운 배열을 생성하여 복사해야 한다
  - 실행 속도를 향상시키기 위해 배열의 크기를 크게 생성할 경우 메모리가 낭비된다
- `비순차적인 데이터`의 `추가/삭제`에 시간이 많이 걸린다
  - 차례대로 데이터를 추가하고 마지막의 데이터를 삭제하는 경우에는 굉장히 빠르나,
    - 배열의 중간에서 값을 제거/추가할 때는 시간이 오래 걸린다

<br>

### Array vs ArrayList & LinkedList

- 배열을 이러한 단점을 가지고 있고, `배열을 통해 List를 구현`한 `ArrayList` 도 위와 같은 문제점들을 가지고 있다
  - 이러한 문제점을 보완하기 위해서 고안된 자료구조가 바로 `LinkedList` 이다
    - 배열은 모든 데이터가 `연속적` 으로 존재하는 반면,
    - `LinkedList` 는 `불연속적`  으로 존재하는 데이터를 서로 연결한 형태로 구성되었다

<br>

## Array 사용하기

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

### 3. 초기화

   : 배열은 생성과 동시에 자동적으로 자신의 타입에 해당하는 기본값으로 초기화되므로 사용하기 전에 따로 초기화를 해주지 않아도 되지만, 원하는 값을 저장하려면 각 요소마다 값을 지정해줘야함

ex)

```java
int num; 
```

- Stack영역에 num이라는 기억공간 만들어줘
- 그리고 여기엔 정수가 들어갈꺼야

<br>

```java
int [] nums = new int[5] ; 
```

배열 선언한 순간 `참조형 (reference type)`이 된다!!!

- stack영역에 nums라는 주소 만들어줘

- new니까 Heap 영역에 int type으로 방 5개 만들어
  - heap이니까 JVM이 관리
  - 그러면 JVM에 의해 5개방에 각각 int 니까 0으로 default 초기화가 일어남

- 한번 이렇게 만들면 resizing 안됨

- 연속적인 공간을 할당 받는다는 보장을 받음

<br>

```java
int [] nums.length ; 
```

- nums라는 배열의 사이즈 어떻게 되니?

<br>

```java
String name; 
```

- Stack영역에 String이라는 기억 공간 만들어줘

- 그리고 여기엔 주소가 들어갈꺼야

<br>

```java
String[] names = new String[5];
```

- reference type!

- JVM에 의해 5개 방이 각각 null으로 default초기화 일어남

<br>

```java
names[0] = “홍길동”;
```

- names의 0번째 방에 코드표 영역의 “홍길동”을 가리키는 주소가 저장됨

<br>

### 4. 배열 복사하기

```java
System.arraycopy(arg0, arg1, arg2, arg3, arg4);
```

**Parameters :**

- source_arr : array to be copied from  (원본 배열)

- sourcePos : starting position in source array from where to copy

- dest_arr : array to be copied in  (복사할 배열)

- destPos : starting position in destination array, where to copy in

- length : total no. of components to be copied.  (원본 배열의 크기)

<br>

### 5. 이차원 배열

- 일차원 배열의 주소를 모아서 만든 배열

- 이차원 배열은 일차원 배열이 가리키는 자료의 주소를 보관한다

- 배열을 생성하면 배열의 각 요소에는 배열요소 타입의 기본값이 자동으로 저장됨

- 2차원 배열은 `행(row)`과 `열(column)`으로 구성되어 있기 때문에 index도 행과 열에 각각 하나씩 존재함
  - 행 index의 범위 = 0~행의 길이 -1
  - 열 index의 범위 = 0~열의 길이 -1

<br>

#### 이차원 배열의 length

```java
int [ ] [ ] score = [5][3];

score.length //==> 5       
//-> score가 참조하고 있는 배열의 길이

score[0].length //==> 3       
//->score[0]가 참조하고 있는 배열의 길이
```

<br>

#### String to char array

: `.toCharArray();`

```java
import java.util.Arrays;

public class JavaStringToCharArray {

 public static void main(String[] args) {
  String str = "Hi Java";

  // get char at specific index
  char c = str.charAt(0);

  // Character array from String
  char[] charArray = str.toCharArray();

  System.out.println(str + " String index 0 character = " + c);
  System.out.println(str + " String converted to character array = " + Arrays.toString(charArray)); 

 }

}
```

<br>

#### (String …) vs String[]

1. (String ...) means you can add as much String param as you want

2. String[] is one parameter which is an array of strings.

<br>

#### Oracle에서 args 실행하기

![img](https://lh3.googleusercontent.com/uGqQh0xF6AbgCvfISK3_liROQRWTzf6W_F__F1W-tJnGakIAnExSAP-kiAUABWS66CIzSviOy-k6xPS-z9tXuM9kNFFn1hZ70fO3kdcDrb7NV2hxCHg_XSs6qBczN-yfYJhZsKZQ)

<br>
