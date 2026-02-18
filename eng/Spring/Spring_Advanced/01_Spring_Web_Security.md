# Spring Web Security

> To celebrate getting back to developing with SpringBoot after a long time, let's organize this again!
>
> References: [bamdule.tistory.com](https://bamdule.tistory.com/52#:~:text=Spring%20Security%EB%8A%94%20%EC%8A%A4%ED%94%84%EB%A7%81%20%EA%B8%B0%EB%B0%98,%EC%99%80%20%EB%B6%84%EB%A6%AC%EB%90%98%EC%96%B4%20%EB%8F%99%EC%9E%91%ED%95%9C%EB%8B%A4), [Book] Learning Spring Web Project through Code

<br>

<br>

## What is Spring Security?

- A framework responsible for application security in Spring-based applications
- Enables simple implementation of user authentication / authorization / security processing!
- Because it operates based on `Filters`, it works separately from **Spring MVC**

<br>

### Security Terms

1. Principal
   - A user accessing an application where the security system is operating
2. Authentication
   - Identifying the accessing user and checking whether they can access the application
3. Authorize (Authorization)
   - Checking whether an authenticated user can use the application's features

<br>

<br>

## How Spring Security Works?

<br>

- Processed using various types of filters and interceptors from Servlet
  - `Filter`
    - A simple filter as referred to in Servlet
    - A Servlet resource independent of Spring
  - `Interceptor`
    - Plays the role of a filter in Spring
    - Managed as a Spring Bean and belongs within the **Spring Context**

<br>

![img](https://docs.spring.io/spring-security/site/docs/current/reference/html5/images/servlet/authorization/filtersecurityinterceptor.png)

<br>

- When using **Spring Security**, a separate **Context** is created and processed using `Interceptor` and `Filter`

- Since Spring Security operates within the current **Spring Context**, it can be designed to enable various authentication methods by utilizing the various beans already included in the context!
