# @AfterReturning

> Reference: [Spring Docs - @AfterReturning](https://docs.spring.io/spring-framework/docs/3.0.0.M4/spring-framework-reference/html/ch07s02.html)

### What is After Returning Advice?

- Executes after the specified method has completed normal execution and returned
  - Executes only when the target method completes normally without throwing an exception
- Mainly used to manipulate the return value of the target method or to perform tasks such as logging

### Options

- `pointcut`

  - Specifies which methods to apply advice to
    - AspectJ pointcut expressions can be used to select methods
  - ex)

    ```java
    @AfterReturning(pointcut = "execution(* com.example.service.MyService.*(..))")
    public void afterReturningAdvice() {
        // advice content
    }
    ```

- `returning`

  - Specifies a variable to receive the return value of the target method
    - Within the advice, the variable can be used to access the target method's return value
  - ex)

    ```java
    @AfterReturning(pointcut = "execution(* com.example.service.MyService.*(..))", returning = "result")
    public void afterReturningAdvice(Object result) {
        // Access the target method's return value through the result variable
    }
    ```

- `argNames`

  - Specifies argument names of the method designated in the pointcut, allowing access to arguments within the advice
    - Can be used when argument names need to be known
  - ex)

    ```java
    @AfterReturning(pointcut = "execution(* com.example.service.MyService.someMethod(..))", returning = "result", argNames = "param1,param2")
    public void afterReturningAdvice(Object result, String param1, int param2) {
        // Access the return value and parameters through result, param1, param2 variables
    }
    ```
