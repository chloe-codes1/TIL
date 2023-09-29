# @IntegrationComponentScan

> Reference: [Spring Docs - IntegrationComponentScan](https://docs.spring.io/spring-integration/api/org/springframework/integration/annotation/IntegrationComponentScan.html)

- Class path scanning을 위해 사용된다
- Spring framework의 `@ComponentScan` 과 비슷한 역할을 하지만, Spring framework의 component mechanism 표준범위 내에서 지원하지 않는 특정 컴포넌트나 annotation을 scan한다
  - ex) [@MessagingGateway](https://docs.spring.io/spring-integration/reference/html/gateway.html#messaging-gateway-annotation)
    - Interface는 `@ComponentScan` annotation이 scan하지 않는데, `@MessagingGateway` 는 interface이므로 해당 annotation을 scan하기 위해 `@IntegrationComponentScan` annotation을 사용한다
