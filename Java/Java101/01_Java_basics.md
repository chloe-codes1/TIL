# Java Basics & Environment Setting

<br/>

### Java의 언어적인 특징 (Features of Java)

- `Simple`

  > C++보다 간단하다  -> 근데 느림
  - Java의 간결하면서도 명료한 객체지향적 설계는 사용자들이 객체지향개념을 보다 쉽게 이해하고 활용할 수 있도록 하여 객체지향 프로그래밍의 저변확대에 크게 기여했다.

- `Object-Oriented`

  - **객체지향 프로그래밍언어** 중 하나로 객체지향개념의 특징인 **상속**, **캡슐화**, **다형성**이 잘 적용된 언어다

- `Memory`

  > Garbage Collection => GC가 메모리 관리!
  - 자바로 작성된 프로그램이 실행되면, **Garbage Collector**가 자동적으로 메모리를 관리해주기 때문에 프로그래머는 메모리를 따로 관리하지 않아도 된다
    - Garbage Collector가 없다면, 프로그래머가 사용하지 않는 메모리를 체크하고 반환하는 일을 수동적으로 처리해야할 것이다.
    - 자동으로 메모리를 관리한다는 것이 다소 비효율적인 면도 있지만, 프로그래머가 보다 프로그래밍에 집중할 수 있도록 도와준다.

- `Robust` (==sturdy)

  - 이 코드가 System을 건드리지 않고 안전하게 돌 것인가.

- `Platform Independent`

  > 운영체제에 독립적이다 (JVM)
  >
  > -> OS 위에 있는 **Java Virtual Machine**이 동작
  - 기존의 언어는 한 운영체제에 맞게 개발된 프로그램을 다른 종류의 운영체제에 적용하기 위해서는 많은 노력이 필요하였지만, Java에서는 더 이상 그런 노력을 하지 않아도 된다
    - 일종의 emulator인 **Java Virtual Machine(JVM)**을 통해서 가능한 것인데,
      - 자바 응용프로그램은 운영체제나 하드웨어가 아닌 **JVM**하고만 통신하고,
      - **JVM**이 자바 응용프로그램으로부터 전달받은 명령을 해당 운영체제가 이해할 수 있도록 **변환**하여 전달한다.
  - 자바로 작성된 프로그램은 운영체제에 독립적이지만, **JVM**은 운영체제에 종속적이어서, 썬에서는 여러 운영체제에 설치할 수 있는 서로 다른 버전의 **JVM**을 제공하고 있다
    - 그래서 자바로 작성된 프로그램은 운영체제와 하드웨어에 관계없이 실행 가능하며 이것을 "한번 작성하면, 어디서나 실행된다 (`Write once, run anywhere`)" 고 표현하기도 한다

- `Multi-Threaded`

  > 자바에서는 운영체제의 도움 없이 프로그램 언어 차원에서 구현
  - 일반적으로 **multi-thread**의 지원은 사용되는 운영체제에 따라 구현 방법도 상이하며, 처리 방식도 다르다.
  - 그러나, Java에서 개발되는 **multi-thread** 프로그램은 시스템과는 관계없이 구현 가능하며, 관련된 library (**Java API**)가 제공되므로 구현이 쉽다.
  - 여러 thread에 대한 **scheduling**을 **Java interpreter**가 담당하게 된다

- `Secured`

  : Java is pretty much "safe" unleses a third party is trying to exploit the JVM

- `Dynamic`

  > 동적 로딩 (Dynamic Loading)을 지원한다
  - 보통 Java로 작성된 application은 여러 개의 class로 구성되어 있다.
  - Java는 **동적 로딩**을 지원하기 때문에 실행 시에 모든 class가 loading 되지 않고, 필요한 시점에 class를 load 하여 사용할 수 있다는 장점이 있다.
  - 일부 class가 변경되어도 전체 application을 다시 compile하지 않아도 되며, application에 변경 사항이 발생해도 비교적 적은 작업만으로도 처리할 수 있는 **유연한 application**을 작성할 수 있다
  
<br>

<br>

### API (Application Programing Interface)

: Java System을 제어하기 위해 Java에서 제공하는 명령어들

 ex) java. (= 최초 버전 -> 코어 API), javaX. (확장 API) 등등…..

- a list of all classes that are part of the Java development kit (JDK). It includes all Java packages, classes, and interfaces, along with their methods, fields, and constructors

<br>

<br>

### JVM (Java Virtual Machine) - 자바 가상 머신

> Java에서는 각각의 운영체제에 맞는 JVM을 제공함
>
> => 컴파일 된 모든 자바 프로그램들은 JVM을 통해 그 어떠한 환경에서도 수정 작업 없이 어디서든 사용 가능!

#### JVM과 속도

- 일반 application의 코드는 `OS`만 거치고 하드웨어로 전달되는데 비해,
  - Java application은 `JVM`을 한 번 더 거치고 하드웨어에 맞게 완전히 compile된 상태가 아니고 **실행 시에 해석(interpret)**되기 때문에 **속도가 느리다**는 단점을 가지고 있다
- 그러나 요즘엔 바이트코드 (compile 된 자바 코드)를 하드웨어의 기계어로 바로 변환해 주는 `JIT 컴파일러`와 향상된 최적환 기술이 적용되어서 속도 격차를 많이 줄였다

<br>

#### JVM의 기능 2가지

1. to allow Java programs to run on any device or operating system
2. to manage and optimize program memory

<br>
<br>

### 람다식(Lambda Expression)

: 메서드를 하나의 '식(expression)'으로 표현한 것.

  -> 메서드를 람다식으로 표현하면 메서드의 이름과 반환값이 없어지므로, 람다식을 '익명 함수(anonymous function)'이라고도 한다.

<br>
<br>

### 자바의 플랫폼

1. `J2SE`  -> 일반적인 데스크탑 PC

​              (JAVA 프로그래밍의 표준이 되는 환경)

2. `J2EE`  -> 서버용 컴퓨터

   (분산환경 지원 / 너무 어렵고, 동작할 수 있게 하는 서버 환경이 고가임)

3. `J2ME`  -> 소형제품 ex) 휴대폰, PDA, 셋탑 박스

<br>

-> (more info from Google)

#### **JAVA SE (Java Platform Standard Edition)**

데스크톱, 서버, 임베디드시스템을 위한 표준 자바 플랫폼. 자바 가상머신 규격 및 API집합을 포함 JAVA EE,ME는 목적에 따라 SE를 기반으로 기존의 일부를 택하거나 API를 추가하여 구성된다. SE는 가장 일반적으로 사용된다. JDBC나 기본적인 기능이 모두 포함되어 있기 때문에 Android개발할때 주로 SE를 사용한다.

#### **JAVA EE (Java Platform EnterPrise Edition)**

자바를 이용한 서버측 개발을 위한 플랫폼. 기존 SE에 웹 애플리케이션 서버에서 동작하는 분산 멀티미디어를 제공하는 자바의 기능을 추가한 서버를 위한 플랫폼. JAVA SE에 서버측을 위한 기능을 부가하였기 때문에 SE기능을 모두 포함한다.

#### **JAVA ME (Java Platform Micro Edition)**

이름에서 알 수 있듯이 임베디드를 위한 자바 플랫폼이다. 자바 플렛폼, 마이크로 에디션의 약자이다. Java ME 또는 J2ME 등으로 불림 제한된 자원을 가진 휴대전화, PDA, 세트톱박스 등에서 Java프로그래밍 언어를 지원하기 위해 만들어진 플랫폼이다

<br>
<br>

### 자바 개발환경 설치

<br>

#### 환경변수 설정하기

<br>

`JAVA_HOME`

`Path`               -> 실행파일을 찾아오는 경로

​                           => 실행 프로그램의 위치만을 나타냄

`Classpath`    -> 클래스를 찾아오는 경로

​                            => 실행 프로그램에서 사용하는 라이브러리의 위치를 나타냄

  => Cl변수값에  .; 입력하면 지금 내가 있는곳을 기준으로 찾는다는 것!

<br>
<br>

*Java는 무조건 Class를 디자인 하는 것이다!*

*Java는 대소문자를 구분한다!*

<br>

#### `public` keyword

```java
public Class  [class명] { }
```

-> Public 넣으면 누구든지 가져다 쓸 수 있다는 뜻

<br>
<br>

#### Main Method

``` java
public static void main(String[] args) {}
```

 => Main function

 -> Java Application을 구동시키는 entry point(=start point) 가 된다

 -> method 이름 뒤에는 무조건 ( ) 가 따라다님 => 괄호가 있으면 함수, 없으면 변수!

- `static` keyword: new keyword 없이 method 선언만으로도 메모리에 올려주는 keyword

- `String`: 데이터 타입 -> 문자열이다

- `args`: 지역변수 (변수명)

- `void`: 콜한 자리에 리턴값(반환값)이 없다는 뜻 -> 이 명령문을 실행하기만 한다는 뜻!

<br>
<br>

### 접근 제한자 (Access Modifier)

  `public` : 모든 접근을 허용
  `protected` : 동일 패키지와 하위 클래스에게 접근 허용
  `default` : 동일 패키지에서 접근 허용
  `private` : 현재 객체 내에서만 허용

<br><br>

### 구분자 (Delimeter)

- class, variable, method를 구분하는 이름

- 중복되면 안된다

- 첫 글자는 영문자, _, $ 가능

- `예약어 (keyword)`는 쓸 수 없다

  ex) class, import, new, public, void, etc.

### Class 안에 들어갈 수 있는 것 2가지

1. Data ( = Variable 변수)

   : 명사는 Data!

2. 기능 (= Method 함수)

   : 동사는 method!     => ~ 하다 붙여서 말되면 동사,,,

    -> 다른 언어에서는 Function이라고 함!

<br>
<br>

### CLI vs GUI

<br>

#### CLI(Command Line Interface)

: 컴퓨터와 사용자가 글자로 명령을 주고 받는 방식 (명령어로 처리하는 환경)

 ex) dos

- 표시 내용이나 입력 내용이 문자 베이스인 사용자 인터페이스

- 아이콘으로 표시하고 마우스 등의 포인터 디바이스로 입력하는 gui에 비해 resource (소프트웨어의 크기나 램의 용량, CPU의 성능)의 소비가 적다

- 작동방식

  : main에서 출발하여 순차적으로 알아서 쭈욱 실행되는 형태

<br>

#### GUI (Graphical User Interface)

: 그래픽 화면에서 버튼을 누르거나 해서 컴퓨터에게 일을 시키는 방식

- 명령어 대신 아이콘을 더블클릭하여 사용하는 환경

- 그래픽 환경에서 작업 하는 것

- 작동방식

  : 사용자가 버튼을 누르거나 어떤 명령을 내릴때 까지 기다리다가

 명령을 받으면 해당 처리를 하는 방식

<br>
<br>

### Cmd (Command Prompt)

 : 명령 프롬포트
      -> CLI(Command Line Interface): 명령을 입력 해야지만 작동함

<br>
<br>

#### 컴파일 명령어

: cmd 창에서 `javac`

 (이 명령어가 제대로 실행되려면 환경변수를 잡아야함)

<br>

ex 1)

```powershell
*javac = java 컴파일 명령어

E: -> e로 들어감

E:\data>javac -d        -> 만들어둔 소스파일을 컴퓨터가 이해할 수 있는 언어로 컴파일해줌 
 => Javac -> 컴파일하라! 는 명령 
 => -d  -> 패키지 기준으로 컴파일하라

  
E:\data>javac -d . Sample.java    => Sample.java 파일을! (컴파일하라)

E:\data>dir             -> directory안에 있는 파일 보기

E:\data 디렉터리

E:\data>java Sample

Hello World!


```

 ex 2)

``` powershell
E:\data>javac -d . Sample.java

E:\data>javac -d ./bin  Sample.java  -> bin이라는 폴더에 따로 관리하려고 넣은 것

E:\data>cd bin   -> cd:  현재 디렉터리 이름을 보여주거나 바꿔줌

E:\data\bin>java Sample  -> main method를 가지고 있는 class name을 써줌

​                                           => 그런데!! 해당 class안에 main 함수가 없으면 오류가 남!



(오류 나면 이렇게 뜸)

E:\data\bin>java Sample

오류: Sample 클래스에서 기본 메소드를 찾을 수 없습니다. 다음 형식으로 기본 메소드를 정의하십시오.

  public static void main(String[] args)

또는 JavaFX 애플리케이션 클래스는 javafx.application.Application을(를) 확장해야 합니다.

```

=>그래서!  `Java App`을 실행하려면 `Main Method`가 있어야 한다!!!!!

<br>
<br>

  \* . : 현재 디렉토리

  \* .. : 이전 디렉토리

<br>
<br>

#### 인코딩 타입 결정하기

**`UTF-8`** -> 전세계의 언어를 모두 포괄할 수 있는 인코딩 타입

 : Eclipse창에서 window - preference-general-appearance-workspace

<br>
<br>

#### Perspective 바꾸기

Eclipse 창 오른쪽에 마우스 올리면

JAVA EE라고 뜸 (Enterprise Edition) -> 서버단임 (too much for us)

 -> 그 옆에 open perspective 에서 Java로 바꿀 수 있음

<br>
<br>

#### Project 만들기

Eclipse는 프로젝트를 먼저 생성 해야함

File - new - java project

<br>
<br>

### Java 소스코드와 클래스 코드는 따로 관리함

  그런데! Eclipse는 자동으로 컴파일을 해서 bin에 저장해줌

<br>

- Src 에 소스가 저장됨

- Bin 에 컴파일 된 소스가 저장됨  -> byte 파일이 저장됨

<br>

#### Project, Package, Class의 위치이동  또는 이름 변경 할 때

: 마우스 오른쪽 -> refactor -> move or rename

<br>

#### 소스코드 확인하기

1. JRE System Library - rt.jar - Java.util - Date.class 들어가거나

2. Eclipse 창에서 class (ex. Date class)위에 마우스 놓고 Ctrl + 클릭 - attach source하면 소스코드 볼 수 있음

<br>
<br>

#### Class

- System Class
- Date Class
- String Class
