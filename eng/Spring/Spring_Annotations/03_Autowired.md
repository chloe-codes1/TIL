# @Autowired

<br>

### What is Autowired?

- An annotation used in the Spring Framework for `automatic injection`
- Spring configures relationships between objects through DI (Dependency Injection), maintaining the application's loose coupling
  - By using the **`@Autowired`** annotation, you can specify that the Spring Container automatically injects the Bean object corresponding to the field, constructor, or method parameter
- Using the @Autowired annotation reduces code complexity and makes maintenance easier, since the Spring Framework automatically injects dependencies without the need to directly create or inject dependent objects

<br>

### Order of Finding Dependent Objects When @Autowired is Applied

1. Search for a bean object with the same type
    - If there is 1, use that bean object
    - If @Qualifier is specified, the bean object must have the same value
2. If there are two or more bean objects with the same type and @Qualifier is not present, find a bean object with the `same name`

    → If found, use that object

3. If there are two or more bean objects with the same type, find the bean object specified by @Qualifier

    → If found, use that object

4. If none of the above cases apply, the container throws an Exception
