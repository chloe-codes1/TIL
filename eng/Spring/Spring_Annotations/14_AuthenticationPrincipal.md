# @AuthenticationPrincipal

> Reference: [Spring Docs - AuthenticationPrincipal](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/core/annotation/AuthenticationPrincipal.html)
>

- An annotation that injects a user object implementing the `UserDetails` interface to retrieve the currently logged-in user
  - What is `UserDetails`?
    - An interface that holds user information (username, password, etc.)
      - Implement this interface to create a class used for login
    - Stored by being encapsulated in `Authentication`
      - In other words, UserDetails implementation information is taken by the Authentication object stored in the Spring Security Context, and user information is contained in the Authentication object

    → Using `@AuthenticationPrincipal`, you can extract user information from the `Authentication` object and have it injected

- Not only `UserDetails` but other classes containing user information can also be injected, because it extracts user information from Spring Security's `Principal` object
  - If the class containing user information implements `Principal`, that class can be used for injection
  - Uses [Authentication.getPrincipal()](https://docs.spring.io/spring-security/site/docs/current/api/org/springframework/security/core/Authentication.html#getPrincipal()) as the method argument!
    - What is `java.lang.Object getPrincipal()`?
      - Retrieves the user information of the principal being authenticated

        ```text
        Returns:
        the Principal being authenticated or the authenticated principal after authentication.
        ```
