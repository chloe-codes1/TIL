# Java Loops & Conditional Statements

<br>

<br>

## Conditional Statements

<br>

### if statement

: An if statement tells the program that it must carry out a specific piece of code if a condition test evaluates to true

```java
if( condition ) {
    statement;
} else{
    statement
}
```

<br>

### switch statement

- a multi-way branch **statement**.
- provides an easy way to dispatch execution to different parts of code based on the value of the expression

```java
switch(인자값) { //조건식이 아닌 인자값!

 //-> 인자값에는 int값으로 promotion이 가능한 데이터 타입만 올 수 있다!

  //ex) 정수형(byte, short, int), 문자형(char)

 

 case 조건값 1:     // => 세미콜론(;) 아니고 콜론(:) 임!!!!!

  수행문; //-> 조건식의 결과가 조건값과 같을 경우 수행될 문장

break;  //=> break를 넣어줘야 제대로 동작함

 case 조건값 2:

  수행문;

break;

case 조건값 3:

  수행문;

break;

case 조건값 4:

  수행문; 

break;

 Default:  //=> default 는 조건이 하나도 맞지 않을 때 빠져나오기 위해!

  수행문;
```

<br><br>

## Loops

<br>

### for loop

- A for loop is divided into three parts, an initialization part, a conditional part and an increment part
- You should sett all initial values in the initialization part of the loop.
- A true from the condition part will execute subsequent statements bounded by {} brackets. A false from the condition part will end the loop.
- For each loop the increment part will be executed.

```java
for (초기식 ; 조건식 ; 증감식) {

 수행문 1;

 수행문 2;

 ….

}
```

<br>

### 다중 for 문

```java
for (초기식1 ; 조건식1 ; 증감식1) {

 for (초기식 2 ; 조건식 2 ; 증감식 2) {

  명령어 2

  }

 명령어 1;

}

명령어 3;
```

<br>

### 향상된 for 문 (enhanced for loop)

: The enhanced for loop can be used to loop over arrays of any type as well as any kind of Java object that implements the java.lang.Iterable interface.

```java
for ( 타입 변수명 : 배열 or 컬렉션) {

 //반복할 문장

}
```

<br>

### while 문

: 선 비교 후 처리

 -> 조건식은 생략 불가! 조건식이 항상 참이 되게 하려면 true를 넣어야함

```java
while (조건식 ) { 

 수행문; -> 조건식의 연산결과가 참(true) 인 동안 반복될 문장들

}
```

<br>

### do ~ while 문

: 조건에 맞지 않아도 일단 1번 실행 한다

```java
do {

 수행문;

} while (조건식); 
```

<br><br>

### break 문

: break를 포함하고 있는 loop(반복문)를 빠져나오는 제어문

 -> break문은 가장 가까운 반복문을 빠져나간다!

```java


for (초기식 ; 조건식 ; 증감식) {



 for(초기식 ; 조건식 ; 증감식){

  수행문;

  break;   //====>내부 for문에서 사용했으므로 내부 for문만 탈출한다

 }

}
```

<br>

<br>

### continue 문

: 어느 특정 문장이나 여러 문장들을 건너뛰고자 할 때 사용

 -> continue 문을 만나면 continue 이하의 수행문들은 처리하지 않고, 다음 반복을 위해 증감식으로 넘어감 (증감식이 없으면 조건식으로!)

<br>

<br>

#### break 문과 continue문의 차이점

 : 반복문을 빠져나가느냐 그렇지 않느냐!

 -> continue문은 반복문을 빠져나가지 않고, 다음 반복 회차 수행을 위해 반복문의 조건식으로 넘어감!

<br>

<br>

#### return문은 function 자체를 종료시키는 것이다
