# @ConfigurationProperties
>
> Reference: [Spring Docs - @ConfigurationProperties](https://docs.spring.io/spring-boot/docs/current/reference/html/features.html#features.external-config)

- `*.properties` , `*.yml` 파일에 있는 property를 자바 클래스에 값을 가져와서 binding 해주는 annotation
- 해당 annotation을 사용하면 여러 표기법에 대해 자동으로 binding 해준다
  - ex)

    | acme.my-project.person.first-name | properties 와 .yml에 권장되는 표기 방법 |
    | --- | --- |
    | acme.myProject.person.firstName | 표준 카멜 케이스 문법. |
    | acme.my_project.person.first_name | .properties와 .yml 에서 사용가능한 방법 ( - 표기법이 더 표준 ) |
    | ACME_MYPROJECT_PERSON_FIRSTNAME | 시스템 환경 변수를 사용할 때 권장 |
- 해당 property 파일을 Bean으로 등록해줘야 정상적으로 동작한다
