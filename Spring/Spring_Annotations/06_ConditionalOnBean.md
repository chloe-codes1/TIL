# @ConditionalOnBean

> Reference: [Spring Docs - @ConditionalOnBean](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnBean.html)
>

<br>

## @ConditionalOnBean 란?

- 해당 조건의 Bean이 BeanFactory에 이미 등록되어 있으면 Bean을 등록한다
- 왜 쓰는가!
  - 작업을 위해 필수적으로 필요한 bean이 미리 생성되어 있는지 확인할 때 사용!

<br>

## @ConditionalOnBean 사용 방법

1. Class Level에 해당 annotation을 추가하여 설정 Class 자체가 Bean 등록 조건에 따라 활성화 / 비활성화될 수 있게 한다
2. Method Level에 해당 annotation을 추가하여 해당 method를 포함하는 Bean이 Bean Factory에 등록되거나 Spring Context에 생성될 조건을 지정한다

<br>

## @ConditionalOnBean 속성

```java
@Target({ ElementType.TYPE, ElementType.METHOD })
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Conditional(OnBeanCondition.class)
public @interface ConditionalOnBean {

    /**
     * The class types of beans that should be checked. The condition matches when beans
     * of all classes specified are contained in the {@link BeanFactory}.
     * @return the class types of beans to check
     */
    Class<?>[] value() default {};

    /**
     * The class type names of beans that should be checked. The condition matches when
     * beans of all classes specified are contained in the {@link BeanFactory}.
     * @return the class type names of beans to check
     */
    String[] type() default {};

    /**
     * The annotation type decorating a bean that should be checked. The condition matches
     * when all the annotations specified are defined on beans in the {@link BeanFactory}.
     * @return the class-level annotation types to check
     */
    Class<? extends Annotation>[] annotation() default {};

    /**
     * The names of beans to check. The condition matches when all the bean names
     * specified are contained in the {@link BeanFactory}.
     * @return the names of beans to check
     */
    String[] name() default {};

    /**
     * Strategy to decide if the application context hierarchy (parent contexts) should be
     * considered.
     * @return the search strategy
     */
    SearchStrategy search() default SearchStrategy.ALL;

    /**
     * Additional classes that may contain the specified bean types within their generic
     * parameters. For example, an annotation declaring {@code value=Name.class} and
     * {@code parameterizedContainer=NameRegistration.class} would detect both
     * {@code Name} and {@code NameRegistration<Name>}.
     * @return the container types
     * @since 2.1.0
     */
    Class<?>[] parameterizedContainer() default {};

}
```

<br>

### Optional Elements

- `value` - Class<?>[]
  - 검증하고자 하는 Bean의 class type들
- `name` - String[]
  - 검증하고자 하는 Bean 이름들을 지정
- `annotation` - Class <? extends Annotation>[]
  - 검증하고자 하는 Bean에 적용된 annotation들을 지정
- `type` - String[]
  - 검증하고자하는 Bean의 type들을 지정
- `search` - [SearchStrategy](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/SearchStrategy.html)
  - Bean의 검색을 제한하는 방법을 설정
  - default 값
    - `SearchStrategy.ALL`: 현재 context와 부모 context 모두 검색
  - 그 외 값
    - `SearchStrategy.CURRENT`: 현재 context만 검색
    - `SearchStrategy.PARENTS`: 부모 context만 검색
- `parameterizedContainer` - Class<?>[]
  - Generic Bean의 존재 여부에 따라 조건을 설정
  - ex)

      ```java
      @ConditionalOnBean(parameterizedContainer = List.class)
      ```

    - Spring Context에 List type의 generic bean이 존재하는지 확인하는 조건을 설정
