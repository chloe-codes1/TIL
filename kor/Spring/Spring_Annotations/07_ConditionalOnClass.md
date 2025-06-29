# @ConditionalOnClass

> Reference: [Spring Docs - @ConditionalOnClass](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/autoconfigure/condition/ConditionalOnClass.html)
>

<br>

## @ConditionalOnClass 란?

- 특정 Class 파일이 존재하면 Bean을 등록한다
- 왜 쓰는가!
  - 해당 annotation이 작성되는 class 의존성에 대한 제어권을 갖지 않는다

<br>

## @ConditionalOnClass 사용 방법

1. Class Level에 해당 annotation을 추가하여 설정 Class 자체가 특정 class 존재 여부에 따라 따라 활성화 / 비활성화될 수 있게 한다
2. Method Level에 해당 annotation을 추가하여 해당 method를 포함하는 Bean이 Classpath에 존재할 조건을 지정한다

<br>

## @ConditionalOnClass 속성

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
  - 존재해야만 하는 class들을 명시
- `name` - String[]
  - 존재해야만 하는 class name들을 명시
