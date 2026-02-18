# @EnableIntegration

> Reference: [Spring Docs - Configuration and @EnableIntegration](https://docs.spring.io/spring-integration/docs/current/reference/html/overview.html#configuration-enable-integration)
>

- When Spring Integration is on the classpath, it is initialized through the `@EnableIntegration` annotation
- Using `@EnableIntegration` allows common components that should be declared only once in the parent context to be used when there is a parent context without Spring Integration Components, or when there are two or more child contexts using Spring Integration
