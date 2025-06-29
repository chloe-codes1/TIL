# Data Types in Java

<br>

## 1. PDT (Primitive Data Type) 

>  데이터 그 자체가 들어가 있는 타입

- 기본 데이터 형  => 딱 8개뿐! 

- 기억 공간에 데이터가 바로 있음

- `. (dot) 연산자`를 쓸 수 없음 => why? 주소가 아니라서!

<br>

### 1. 논리형  

- `boolean`  

  : 1bit
  
   (true/false) -> JAVA는 0,1 허용하지 않음

<br>

### 2. 문자형

- `char `    

  : 2byte

  ex) ‘a’ -> 문자 하나만 가능
  
   => single quotation(‘’) 사용!! -> ASCII code 값으로 저장됨

<br>

`+`   

**byte**     ==  8bit (1 byte)  ==  -128 ~127

<br>

### 3. 정수형 

- `Short` 

  : 16 bit (2 byte)

-  `Int`  

  : 32bit (4 byte)  => 정수형의 기본은 Int

- `Long`  

  : 64bit (8 byte)

<br>

### 4. 실수형   

- `float`      

  : 32bit (4 byte)

- `Double`       

  : 64bit (8 byte)   => 실수형의 기본은 Double

<br>



-> *위의 8개 제외하고는 다 Reference Type!!!!!*

<br><br>

## 2. Reference Type 

> 주소가 들어가 있는 타입

: 참조 데이터 형

- 기억 공간에 주소가 들어가고 주소를 찾아 들어가야지만 실질적인 데이터가 있음

- `. (dot) 연산자` 쓸 수 있음!!  ex) 주소.

- Reference형에서는 String 빼고는 다 new 써야함

- String은 기본형처럼 쓸 수도 있고, new 쓸 수도 있음!!
  - New는 Heap영역에 올라감

  - 기본형 처럼 쓰면 new가 아닌 다른 영역에 올라감 => 이게 데이터 소모가 적음!

    ex) String address = new String(“비트캠”);  -> new 썼을 때

    ​       String address = “비트캠”;   -> 기본형처럼 썼을 때

<br>

<br>

#### String은 immutable한 (불변의) 객체이다!

 -> 그래서 String 의 데이터를 바꾸려면 String Builder나 String Buffer를 써야 함

<br>

#### Buffer 

= temporary 한 기억공간 (임시 공간)

 <br>

 #### null 값 

= 참조형에서 주소가 없는것을 명시적으로 알려주는 값

   ex) now = null;

<br>

<br>

#### Java는 연산자를 기준으로  type을 일치시키려고 함!!

 ex 1)

```
 1 / 2 => 0

 1 / 2. => 0.5
```

   -> 실수형으로 type을 일치 시킴 (1을 1.0으로)

​	=> 정수형에서 실수형으로 바꾸는 과정에서 데이터 손실이 없으므로 자동으로 `type promotion` 일어남

<br>

ex 2)

```
int a = 1 + 1;   = 2

String b = “1” + “1”;  = “11”         

String c = 1 +1 + 1 + “1”  = “31”
```

 -> 결과값이 문자열이므로 타입을 String으로 선언함

​	=> 결과 값이 무엇이냐에 따라 타입이 달라진다!

<br>

<br>

#### char type & int type

`char type`은  `int type`으로 자동 *promotion*이 발생함!

 => but, int를 char로 바꾸려면 *type casting*을 해야함   

-> why? 데이터 소모가 있기 때문!

​     : char 2 byte    <   int 4 byte

<br>

*큰 사이즈에서 작은 사이즈로 가려면 데이터 소모가 있으므로 type casting을 해라!*



<br>

#### (정리)

큰 사이즈 -> 작은 사이즈 => 데이터 소모 있음 ⇒ `Type Casting`

작은 사이즈 -> 큰 사이즈 => 데이터 소모 없음 ⇒ `Promotion`

<br><br>



#### (Type Promotion in JAVA)

![img](https://lh3.googleusercontent.com/KXOWKRk-kEyIoztoda2M7RfldyM5UmDQKPNULtwcq5_UduHG7bhd9DFu1aaVHlGdLSgs91bdaQiKdPpygaduHFRi5Ew2pF6_kIHPhOKqc4jXuRI0ZUsQ0vEI3fXAd05i7YOmpMEF)

<br>
