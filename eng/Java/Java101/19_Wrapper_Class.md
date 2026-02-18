# Wrapper Class
>
> Boxing and Unboxing, AutoBoxing
>

<br>

### Intro

In Java, there are primitive data types and Wrapper classes

- `Primitive data types`: int, long, float, double, boolean, etc.
- `Wrapper classes`: Integer, Long, Float, Double, Boolean, etc.

<br>

### Boxing & Unboxing

- `Boxing`
  - Converting a Primitive data type to a Wrapper class

    ```java
    int n = 100;
    Integer num = new Integer(n);
    ```

- `Unboxing`
  - Converting a Wrapper class to a Primitive data type

    ```java
    Integer num = new Integer(100);
    int n = num.intValue();
    ```

<br>

### Auto Boxing

- Since JDK 1.5, the Java compiler automatically performs conversion when boxing and unboxing are needed -> `Auto Boxing & Auto Unboxing`
  - This feature is only available when there is a corresponding `Primitive data type` for each Wrapper class

    ```java
    // Auto Boxing
    int n = 100;
    Integer num = n;

    // Auto Unboxing
    Integer num = new Integer(100);
    int n = num;
    ```

- Caution: `Performance`
  - Although Auto Boxing and Auto Unboxing are provided for convenience, since additional computation work is needed internally, it is better to implement `same-type operations` so that `Auto Boxing & Auto Unboxing` does not occur
