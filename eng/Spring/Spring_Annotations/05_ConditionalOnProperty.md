# @ConditionalOnProperty

> Reference: [Spring Docs - @ConditionalOnProperty](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnProperty.html)
>

<br>

## What is @ConditionalOnProperty?

- A conditional annotation used in the Spring Framework to specify conditions under which a Bean is created or configured
- Can determine whether to create a Bean based on the presence or value of a specific property

<br>

## Attributes of @ConditionalOnProperty

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

- The property exists in the [Environment](https://docs.spring.io/spring-framework/docs/6.0.11/javadoc-api/org/springframework/core/env/Environment.html), and
- is not false

<br>

### Optional Elements

- `name` (required attribute) - String[]
  - Specifies the name of the property to test
- `havingValue` - String
  - Specifies the attribute that the property should have
    - Specifies a value to compare with the property value!
  - Can be used optionally, with a default value of empty string ("")
  - If this value is not specified or created as an empty string, the Bean is created as long as the property is set, regardless of the property value
  - If a value is specified (not empty string), the Bean is created only when the specified value matches the property value
- `matchIfMissing` - boolean
  - Determines whether the condition is satisfied when the property does not exist in the Environment at all
  - Default value is `false`, and the Bean is not created if the property is not set
  - When set to `true`, the Bean is created even if the property is not set
- `prefix` - String
  - Specifies a prefix to apply to each property
  - This attribute allows specifying conditions using a common prefix for multiple properties
- `value` - String[]
  - Alias for name()
