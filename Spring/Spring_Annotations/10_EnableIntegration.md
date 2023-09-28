# @EnableIntegration

> Reference: [Spring Docs - Configuration and @EnableIntegration](https://docs.spring.io/spring-integration/docs/current/reference/html/overview.html#configuration-enable-integration)
>

- Class path에 Spring Integration이 있으면, `@EnableIntegration` annotation을 통해 초기화된다
- `@EnableIntegration` 을 사용하여 Spring Integration Component가 없는 부모 context를 가졌거나 Spring Integration을 사용하는 2개 이상의 자식 context를 가졌을때, 부모 context에서 한 번만 선언되어야 할 공통 component를 사용할 수 있게 해준다
