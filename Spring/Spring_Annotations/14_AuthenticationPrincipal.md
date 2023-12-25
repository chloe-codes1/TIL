# @AuthenticationPrincipal

> Reference: [Spring Docs - AuthenticationPrincipal](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/core/annotation/AuthenticationPrincipal.html)
>

- 현재 로그인한 유저를 가져오기 위해 `UserDetails` 인터페이스를 구현한 유저 객체를 주입하는 annotation
  - `UserDetails` 란?
    - 사용자 정보 (username, password 등)을 가지는 interface
      - 해당 interface를 구현하여 로그인에 사용할 class를 만들면 된다
    - `Authentication` 으로 캡슐화하여 저장된다
      - 즉, UserDetails 구현체 정보는 Spring Security Context에 저장된 Authentication 객체가 가져가고, 사용자 정보는 Authentication 객체에 담겨 있다

    → `@AuthenticationPrincipal` 을 사용하면 `Authentication` 객체에서 사용자 정보를 추출해서 주입받을 수 있다

- `UserDetails` 뿐만 아니라 다른 사용자 정보를 담은 class도 주입받을 수 있는데, 이것은 Spring Security의 `Principal` 객체에서 사용자 정보를 추출하여 주입받기 때문이다
  - 사용자 정보를 담은 class가 `Principal` 을 구현하고 있다면 해당 class를 사용하여 주입받을 수 있다
  - [Authentication.getPrincipal()](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/core/Authentication.html#getPrincipal())  를 method argument로 사용한다!
    - `java.lang.Object getPrincipal()` 란?
      - 인증되는 주체의 사용자 정보를 가져온다

        ```text
        Returns:
        the Principal being authenticated or the authenticated principal after authentication.
        ```
