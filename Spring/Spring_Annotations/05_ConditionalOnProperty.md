# @ConditionalOnProperty

> Reference: [Spring Docs - @ConditionalOnProperty](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnProperty.html)
>

<br>

## @ConditionalOnProperty 란?

- Spring Framework에서 어떤 Bean이 생성되거나 구성되기 위한 조건을 지정하는데 사용되는 조건부 annotation
- 특정 property 값의 유무나 값에 따라 Bean 생성 여부를 결정할 수 있다

<br>

## @ConditionalOnProperty 의 속성

```java

@Retention(RetentionPolicy.RUNTIME)
@Target({ ElementType.TYPE, ElementType.METHOD })
@Documented
@Conditional(OnPropertyCondition.class)
public @interface ConditionalOnProperty {

    /**
     * Alias for {@link #name()}.
     * @return the names
     */
    String[] value() default {};

    /**
     * A prefix that should be applied to each property. The prefix automatically ends
     * with a dot if not specified. A valid prefix is defined by one or more words
     * separated with dots (e.g. {@code "acme.system.feature"}).
     * @return the prefix
     */
    String prefix() default "";

    /**
     * The name of the properties to test. If a prefix has been defined, it is applied to
     * compute the full key of each property. For instance if the prefix is
     * {@code app.config} and one value is {@code my-value}, the full key would be
     * {@code app.config.my-value}
     * <p>
     * Use the dashed notation to specify each property, that is all lower case with a "-"
     * to separate words (e.g. {@code my-long-property}).
     * @return the names
     */
    String[] name() default {};

    /**
     * The string representation of the expected value for the properties. If not
     * specified, the property must <strong>not</strong> be equal to {@code false}.
     * @return the expected value
     */
    String havingValue() default "";

    /**
     * Specify if the condition should match if the property is not set. Defaults to
     * {@code false}.
     * @return if the condition should match if the property is missing
     */
    boolean matchIfMissing() default false;

}
```

### Default value

- property가 [Environment](https://docs.spring.io/spring-framework/docs/6.0.11/javadoc-api/org/springframework/core/env/Environment.html) 에 존재하고,
- false가 아니다

<br>

### Optional Elements

- `name` (필수 속성) - String[]
  - test 하고자 하는 property 의 이름을 지정한다
- `havingValue` - String
  - 해당 property가 가지고 있어야 하는 attribute를 명시한다
    - property 값과 비교할 값을 지정!
  - 선택적으로 사용할 수 있으며, default 값은 empty string (””)이다
  - 해당 값이 지정하지 않거나 empty string으로 생성하면, property 값이 어떤 값이든 상관 없이 property가 설정되기만 하면 Bean이 생성된다
  - 값이 지정된 경우 (not empty string), 지정한 값과 property 값이 일치해야 Bean이 생성된다
- `matchIfMissing` - boolean
  - 해당 property 가 아예 Environment에 존재하지 않을 때 조건을 만족할지 여부를 결정한다
  - default 값은 `false` 이고, property가 설정되지 않으면 Bean이 생성되지 않는다
  - `true` 로 설정하면 property가 설정되지 않은 경우에도 Bean이 생성된다
- `prefix` - String
  - 각각의 property에 적용하고자 하는 prefix를 지정한다
  - 이 속성을 사용하면 여러 property들에 대해 공통된 prefix를 사용하여 조건을 지정할 수 있다
- `value` - String[]
  - name() 의 alias
