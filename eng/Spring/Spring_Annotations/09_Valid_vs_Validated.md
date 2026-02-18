# @Valid vs @Validated

> Reference:[Baeldung - Differences in @Valid and @Validated Annotations in Spring](https://www.baeldung.com/spring-valid-vs-validated)

## @Valid and @Validated

When applying `@Valid`, `all validation` is performed on attributes with constraint conditions set.
If you want to keep the constraint conditions declared but **`only validate specific attributes`**, you can use `@Validated`

## @Valid vs  @Validated

### Target

> `@Validated` includes the functionality of `@Valid`
>
>
> →  Anywhere `@Valid` is applied can be replaced with `@Validated`
>
- `@Valid`
  - Used to perform validation on parameters or objects within methods
  - Not used for class-level validation
- `@Validated`
  - Supports both method-level validation and class-level validation

### Group Validation Support

- `@Valid`
  - Does not support group validation
- `@Validated`
  - Can specify groups of validation options to review
  - Can be used to apply or skip validation for specific groups

### Validation Method

- `@Valid`
  - **javax.validation.Validator**
- `@Validated`
  - **org.springframework.validation.Validator**
    - Integrated with Spring's validation methods
    - When using the `@Validated` annotation, Spring utilizes Validator implementations to perform validation on the corresponding object

### Exception Handling

- `@Valid`
  - **javax.validation.ConstraintViolationException** is thrown
- `@Validated`
  - Spring's **MethodArgumentNotValidException** or **BindException** may be thrown, and custom messages or handlers can be configured to handle these exceptions
