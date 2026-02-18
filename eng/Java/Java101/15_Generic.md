# Generic

<br>

- Generic can be said to be responsible for `safety` in Java
- It is used in `methods` or `collection classes` that handle objects of various types, and it is a feature that performs `type checking` during the compilation process
- Since the object's `type is checked at compile time`, it increases the type safety of objects and reduces the hassle of `type casting`
  - Naturally, the code also becomes more concise
- ex)
  - Generic is what allows `only specific objects to be added to a Collection`, or only objects with characteristics of a specific class to be added
    - The advantage of this is that there is `no need to implement separate logic inside the collection to verify whether the incoming value is the value you want`
  - It enables `clearer communication of intent` in API design
