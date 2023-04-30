# Interceptor vs AOP vs Filter

<br>

## Interceptor

- Spring이 제공하는 기술
- `디스패처 서블릿(Dispatcher Servlet)`이 `컨트롤러`를 `호출`하기 전과 후에 요청과 응답을 참조하거나 가공할 수 있는 기능을 제공
- `Spring Context` 에서 동작

## Interceptor vs AOP

- Interceptor 대신에 Controller들에 적용할 부가 기능을 advice로 만들어 `AOP`(Aspect Oriented Programming, 관점 지향 프로그래밍)를 적용할 수도 있다
- but, 아래의 이유들로 `컨트롤러의 호출 과정`에 적용되는 `부가 기능`들은 Interceptor를 사용하는게 낫다
    1. Spring의 컨트롤러는 타입과 실행 method가 모두 제각각이라 `Pointcut` (적용할 method 선별)의 작성이 어렵다
    2. Spring의 Controller는 parameter나 return 값이 일정하지 않다

## Filter

- `Dispatcher Servlet`에 요청이 전달되기 전/후에 URL pattern 에 맞는 모든 요청에 대해 `부가 작업`을 처리할 수 있는 기능을 제공한다
- Dispatcher Servlet은 Spring의 가장 앞단에 존재하는 Front controller 이므로, Filter는 `Spring 범위 밖`에서 처리 된다
  - Filter는 `Web context` 에서 동작한다
