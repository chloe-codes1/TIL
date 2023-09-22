# Wrapper Class
>
> Boxing과 Unboxing, AutoBoxing
>

<br>

### Intro

Java에는 기본 자료형과 Wrapper class가 존재한다

- `기본 자료형(Primitive data type)`: int, long, float, double, boolean 등
- `Wrapper class`: Integer, Long, Float, Double, Boolean 등

<br>

### Boxing & Unboxing

- `Boxing`
  - Primitive data type → Wrapper class로 만드는 것

    ```java
    int n = 100;
    Integer num = new Integer(n);
    ```

- `Unboxing`
  - Wrapper class → Primitive data type으로 변환

    ```java
    Integer num = new Integer(100);
    int n = num.intValue();
    ```

<br>

### Auto Boxing

- JDK 1.5부터는 Java 컴파일러가 박싱과 언박싱이 필요한 상황에 자동으로 변환을 해준다 → `Auto Boxing & Auto Unboxing`
  - 이 기능은 각 Wrapper class에 상응하는 `Primitive data type` 일 경우에만 가능하다

    ```java
    // 오토 박싱
    int n = 100;
    Integer num = n;
    
    // 오토 언박싱
    Integer num = new Integer(100);
    int n = num;
    ```

- 주의할 점: `성능`
  - 편의성을 위해 Auto Boxing과 Auto Unboxing이 제공되고 있지만, 내부적으로 추가 연산 작업이 필요하기 때문에  `Auto Boxing & Auto Unboxing` 이 일어나지 않도록 `동일 타입 연산` 이 이루어지도록 구현하는 것이 좋다
