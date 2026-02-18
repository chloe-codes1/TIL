# Lombok

## What is Lombok?

It automatically generates frequently used code during development such as Getter, Setter, default constructor, toString, etc. using annotations

## Lombok Annotations

### @Getter

Generates get methods for all fields declared within a class

### @RequiredArgsConstructor

- Generates a constructor with all `final` fields as arguments
  - Fields without final are not included in the constructor
- Reason for use
  - To solve the inconvenience of having to continuously modify constructor code every time the dependency relationship of the class changes

### @NoArgsConstructor

- Generates a default constructor
- Has the same effect as `public Post() {}`

### @Builder

- Creates a Builder pattern class for the corresponding Class
- When declared at the top of a Class, only fields included in the constructor are included in the builder
- Options
  - `toBuilder`
    - default = false
    - When set to true, you can call the `toBuilder()` method on an instance created with the builder to create a new instance via the Builder Pattern based on that instance's values
