# @AfterReturning

> Reference: [Spring Docs - @AfterReturning](https://docs.spring.io/spring-framework/docs/3.0.0.M4/spring-framework-reference/html/ch07s02.html)

### After returning advice 란?

- 지정한 method의 실행이 정상적으로 실행되고 return 한 후 실행된다
  - target method가 예외를 던지지 않고 정상적으로 실행된 경우에만 실행된다
- 주로 target method의 return 값을 조작하거나, logging과 같은 작업을 수행하는 데 사용된다

### Options

- `pointcut`

  - 어떤 method에 대해 advice를 적용할 것인지 지정한다
    - AspectJ의 pointcut 표현식을 사용하여 method를 선택할 수 있다
  - ex)

    ```java
    @AfterReturning(pointcut = "execution(* com.example.service.MyService.*(..))")
    public void afterReturningAdvice() {
        // advice 내용
    }
    ```

- `returning`

  - target method의 return 값을 받을 변수를 지정한다
    - advice 내에서 해당 변수를 사용하여 target method return 값에 접근할 수 있다
  - ex)

    ```java
    @AfterReturning(pointcut = "execution(* com.example.service.MyService.*(..))", returning = "result")
    public void afterReturningAdvice(Object result) {
        // result 변수를 통해 대상 method의 return 값에 접근 가능
    }
    ```

- `argNames`

  - pointcut에서 지정한 method의 argument 이름을 지정하여 advice 내에서 argument에 접근할 수 있게 한다
    - argument 이름을 알아야 하는 경우 사용할 수 있다
  - ex)

    ```java
    @AfterReturning(pointcut = "execution(* com.example.service.MyService.someMethod(..))", returning = "result", argNames = "param1,param2")
    public void afterReturningAdvice(Object result, String param1, int param2) {
        // result, param1, param2 변수를 통해 return 값과 parameter 에 접근 가능
    }
    ```
