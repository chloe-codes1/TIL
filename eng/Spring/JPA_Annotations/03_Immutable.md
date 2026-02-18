# @Immutable

> Reference: [@Immutable in Hibernate](https://www.baeldung.com/hibernate-immutable)
>

### What is @Immutable?

- When this annotation is added to an `Entity`, updates will not work
- When added to a `Collection`, add & delete will not work

### Behavioral Changes When @Immutable Annotation is Added

- INSERT
  - No changes
- UPDATE
  - Hibernate does not throw an exception and simply `ignores` the UPDATE operation execution
  - Separate configuration is needed to trigger an exception
- DELETE
  - No changes

### Things to Note

- `@Immutable` entities can still be updated via JPQL or Criteria
- However, starting from **5.2.17**, updates have been blocked but only a WARNING is logged
  - To also trigger an error, set the following property

    ```java
    hibernate.query.immutable_entity_update_query_handling_mode=exception
    ```
