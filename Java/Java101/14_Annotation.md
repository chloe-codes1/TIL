# Annotation

<br>

## Annotation의 특징

- Annotation이란 본래 주석이란 뜻으로, interface를 기반으로 한 문법이다
  - 주석과는 그 역할이 다르지만 주석처럼 코드에 달아 class에 특별한 의미를 부여하거나 기능을 주입할 수 있다
- Annotation을 사용하면 데이터에 대한 `유효성 검사조건`을 annotation을 사용하여 직접 명시함으로써 유효 조건을 쉽게 파악할 수 있게 되며, 코드가 깔끔해진다
- Annotation은 크게 `문서화`, `compiler 체크`, `코드 분석` 을 위한 용도로 사용된다
  - 문서화 부분은 `JavaDoc` 이 있기 때문에 많이 사용되지는 않는다
  - Annotation의 본질적인 목적은 소스 코드에 메타데이터를 표현하는 것이다
- 해석되는 시점을 정할 수도 있다 (`Retention Policy`)
  
<br>

## Annotation의 종류
>
> Annotation에는 크게 세 가지 종류가 존잰한다
>

### 1. JDK 에 내장되어 있는 `Built-in annotation`

- 주로 compiler를 위한 것으로, compiler에게 유용한 정보를 제공한다
- ex)
  - `@Override`

    > 상속받아서 메소드를 override 할 때 나타나는 `@Override` annotation
    >
    - method 앞에만 붙일 수 있으며, 현재 method가 super class의 method를 override한 method임을 compiler에게 명시한다
    - overriding 할 때 method 명에서 오타가 발생할 수 있는데 compiler 입장에서는 새로운 method를 생성하는 것인지 overriding 하는 것인지 모른다
      - 이런 경우 annotation을 통해서 오타가 발생할 수 있는 부분을 잡아줄 수 있다
  - **`@Deprecated`**
    - 차후 버전에 지원되지 않을 수 있기 때문에 더 이상 사용되지 말아야 할 메소드를 나타낸다.
  - **`@SupressWarning`**
    - 프로그래머의 의도를 compiler에게 전달하여 경고를 제거한다
  - **`@FunctionalInterface`**
    - compiler에게 다음의 인터페이스는 함수형 인터페이스라는 것을 알린다
    - overriding annotation과 같은 이유로 실수를 미연에 방지하기 위해 사용한다

<br>

### 2. annotation에 대한 정보를 나타내기 위한 annotation인 `Meta annotation`

- annotation에 사용되는 annotation으로 해당 annotation의 동작대상을 결정한다
  - 주로 새로운 annotation을 정의할 때 사용한다
- ex)
  - `@Target`
    - annotation이 적용 가능한 대상을 지정하는데 사용한다
    - 여러 개의 값을 지정할 때는 배열에서 처럼 괄호 { }를 사용해야 한다
  - `@Retention`
    - 커스텀 annotation을 생성할 때 주로 사용하는 annotation으로, 어느 시점까지 annotation의 memory를 가져갈 지 설정할 수 있다
      - **annotation의 `life cycle`을 설정**하는 것으로, 즉, annotation이 언제까지 살아 있을지를 정하는 것!
    - `속성`
      - `RetentionPolicy`
        - Retention Policy 란?
          - Annotation의 수명 주기를 정의하는 정책
            - Compile 된 class file에서 annotation 정보를 유지할지 여부를 지정하는데 사용된다
        - Retention Policy의 종류
          - `RetentionPolicy.SOURCE`
            - source code (.java)까지 남아있는다
              - compile 과정에서 annotation 정보가 사라진다
            - 주로 compiler 경고나 error message를 생성하는데 사용된다
          - `RetentionPolicy.CLASS`
            - class 파일(.class)까지 남아있는다 (=bytecode)
              - runtime 시 유지되지 않는다
            - 주로 compile 시에 코드 생성을 하거나, compiler의 처리를 위해 사용된다
          - `RetentionPolicy.RUNTIME`
            - runtime까지 남아있는다 (=사실상 안 사라진다)
            - 주로 runtime 시에 `reflection` 을 통해 annotation 정보를 읽거나 수정하는데 사용된다
              - ex) 특정 annotation을 사용하여 runtime 시에 class의 동작을 변경하거나 추가하는 기능을 제공
  - `@Inherited`
    - annotation이 자식 class에도 상속되도록 하는 annotation이다
    - 이 annotation을 부모 class에 붙이면 자식 class도 이 annotation이 붙은 것과 같이 인식된다
  - `@Native`
    - Native method에 의해 참조되는 상수 필드에 붙이는 annotation이다
      - Native method란 JVM이 설치된 OS의 method를 말한다
      - Native method는 보통 C언어로 작성되어 있고, Java에서는 method의 선언부만 정의하고 구현은 하지 않는다
      - Object class의 method들은 대부분 Native method이다
      - 우리는 Java라는 언어를 통해 OS의 method를 호출하고 있었던 것이다
      - Native method와 Java에 정의된 method를 연결하는 것을 `JNI(Java Native Interface)`라고 한다

<br>

### 3. 개발자가 직접 만들어 내는 `Custom Annotation`
