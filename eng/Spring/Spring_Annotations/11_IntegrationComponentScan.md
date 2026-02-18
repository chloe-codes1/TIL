# @IntegrationComponentScan

> Reference: [Spring Docs - IntegrationComponentScan](https://docs.spring.io/spring-integration/api/org/springframework/integration/annotation/IntegrationComponentScan.html)

- Used for classpath scanning
- Plays a similar role to Spring Framework's `@ComponentScan`, but scans specific components or annotations that are not supported within the standard scope of Spring Framework's component mechanism
  - ex) [@MessagingGateway](https://docs.spring.io/spring-integration/reference/html/gateway.html#messaging-gateway-annotation)
    - Interfaces are not scanned by the `@ComponentScan` annotation, and since `@MessagingGateway` is an interface, the `@IntegrationComponentScan` annotation is used to scan this annotation
