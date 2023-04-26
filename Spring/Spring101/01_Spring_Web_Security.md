# Spring Web Security

> 오랜만에 SpringBoot로 개발하게 된 기념으로(?) 다시 정리하기!
>
> References: [bamdule.tistory.com](https://bamdule.tistory.com/52#:~:text=Spring%20Security%EB%8A%94%20%EC%8A%A4%ED%94%84%EB%A7%81%20%EA%B8%B0%EB%B0%98,%EC%99%80%20%EB%B6%84%EB%A6%AC%EB%90%98%EC%96%B4%20%EB%8F%99%EC%9E%91%ED%95%9C%EB%8B%A4), [책] 코드로 배우는 스프링 웹 프로젝트

<br>

<br>

## What is Spring Security?

- Spring 기반의 application 보안을 담당하는 framework
- 사용자 인증 / 권한 / 보안처리를 간단하게 구현할 수 있게 해준다!
- `Filter` 기반이라서 동작하기 때문에 **Spring MVC**와는 분리되어 동작

<br>

### Security Terms

1. Principal (접근 주체)
   - 보안 시스템이 작동되고 있는  application에 접근하는 user
2. Authentication (인증)
   - 접근한 user를 식별하고, application에 접근할 수 있는지 검사
3. Authorize (인가)
   - 인증된 user가 application의 기능을 이용할 수 있는지 검사

<br>

<br>

## How Spring Security Works?

<br>

- Servlet의 여러 종류의 filter와 interceptor 를 이용해서 처리됨
  - `Filter`
    - Servlet 에서 말하는 단순한 필터
    - Spring 과는 무관하게 Servlet 자원임
  - `Interceptor`
    - 스프링에서 필터와 역할을 함
    - Spring의 Bean으로 관리되면서 **Spring Context** 내에 속함

<br>

![img](https://docs.spring.io/spring-security/site/docs/current/reference/html5/images/servlet/authorization/filtersecurityinterceptor.png)

<br>

- **Spring Security**를 이용하게 되면 `Interceptor`와 `Filter`를 이용하여 별도의 **Context**를 생성해 처리됨

- Spring Security는 현재 동작하는 **Spring Context** 내에서 동작하기 때문에 이미 context에 포함된 여러 빈들을 같이 이용해서 다양한 방식의 인증 처리가 가능하도록 설계할 수 있다!
