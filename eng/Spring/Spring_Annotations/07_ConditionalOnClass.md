# @ConditionalOnClass

> Reference: [Spring Docs - @ConditionalOnClass](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnClass.html)
>

<br>

## What is @ConditionalOnClass?

- Registers a Bean if a specific Class file exists
- Why use it!
  - The class where this annotation is written does not have control over the dependency

<br>

## How to Use @ConditionalOnClass

1. Add the annotation at the Class Level so that the configuration Class itself can be activated/deactivated based on the existence of a specific class
2. Add the annotation at the Method Level to specify conditions under which the Bean containing that method exists on the Classpath

<br>

## @ConditionalOnClass Attributes

```java
@Target({ ElementType.TYPE, ElementType.METHOD })
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Conditional(OnClassCondition.class)
public @interface ConditionalOnClass {

    /**
     * The classes that must be present. Since this annotation is parsed by loading class
     * bytecode, it is safe to specify classes here that may ultimately not be on the
     * classpath, only if this annotation is directly on the affected component and
     * <b>not</b> if this annotation is used as a composed, meta-annotation. In order to
     * use this annotation as a meta-annotation, only use the {@link #name} attribute.
     * @return the classes that must be present
     */
    Class<?>[] value() default {};

    /**
     * The classes names that must be present.
     * @return the class names that must be present.
     */
    String[] name() default {};

}
```

<br>

### Optional Elements

- `value` - Class<?>[]
  - Specifies the classes that must exist
- `name` - String[]
  - Specifies the class names that must exist
