# @ConfigurationProperties
>
> Reference: [Spring Docs - @ConfigurationProperties](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.external-config)

- An annotation that retrieves and binds property values from `*.properties` or `*.yml` files to Java classes
- Using this annotation automatically handles binding for various notation styles
  - ex)

    | acme.my-project.person.first-name | Recommended notation for properties and .yml |
    | --- | --- |
    | acme.myProject.person.firstName | Standard camel case syntax. |
    | acme.my_project.person.first_name | Notation usable in .properties and .yml (dash notation is more standard) |
    | ACME_MYPROJECT_PERSON_FIRSTNAME | Recommended when using system environment variables |
- The property file must be registered as a Bean for it to work properly
