# @ConditionalOnBean

> Reference: [Spring Docs - @ConditionalOnBean](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnBean.html)
>

<br>

## What is @ConditionalOnBean?

- Registers a Bean if the Bean matching the condition is already registered in the BeanFactory
- Why use it!
  - Used to verify that a Bean that is essentially required for the task has been created in advance!

<br>

## How to Use @ConditionalOnBean

1. Add the annotation at the Class Level so that the configuration Class itself can be activated/deactivated based on Bean registration conditions
2. Add the annotation at the Method Level to specify conditions under which the Bean containing that method is registered in the Bean Factory or created in the Spring Context

<br>

## @ConditionalOnBean Attributes

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
  - The class types of the Beans to verify
- `name` - String[]
  - Specifies the names of the Beans to verify
- `annotation` - Class <? extends Annotation>[]
  - Specifies the annotations applied to the Beans to verify
- `type` - String[]
  - Specifies the types of the Beans to verify
- `search` - [SearchStrategy](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/SearchStrategy.html)
  - Configures how to limit Bean searching
  - Default value
    - `SearchStrategy.ALL`: Search both the current context and parent context
  - Other values
    - `SearchStrategy.CURRENT`: Search only the current context
    - `SearchStrategy.PARENTS`: Search only parent contexts
- `parameterizedContainer` - Class<?>[]
  - Sets conditions based on the existence of generic Beans
  - ex)

      ```java
      @ConditionalOnBean(parameterizedContainer = List.class)
      ```

    - Sets a condition to check whether a generic bean of type List exists in the Spring Context
