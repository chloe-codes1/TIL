# Optional Class

> java.util.Optional<T> Class
>

<br>

### What is the Optional<T> class?

- The `Optional<T>` class is a `Wrapper class` that wraps objects of type 'T', like the Integer or Double classes
  - Therefore, an Optional instance can store reference variables of all types
- Using Optional objects can simplify unexpected `NullPointerException`
  - That is, exceptions caused by null values can be handled without complex conditional statements

<br>

### Creating Optional Objects

Optional objects can be created using the `of()` method or the `ofNullable()` method

- `of() method`
  - Returns an Optional object with a specified non-null value
  - If null is stored in an Optional object created through the of() method, a `NullPointerException` will be thrown
- `ofNullable() method`
  - If there is a possibility that the reference variable's value could be null, it is better to create an Optional object using the ofNullable() method
  - The ofNullable() method:
    - Returns an Optional object with the specified value if the value is not null,
    - Returns an empty Optional object if the specified value is null
