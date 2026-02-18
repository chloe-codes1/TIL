# Final Keyword
>
> The common characteristic of the final keyword is that attaching it means restricting something
>

<br>

### Final Class

- Other classes `cannot inherit` from it
- The String class is also final!
  - Attempting to inherit the String class will cause an error

<br>

### Final Method

- Other methods `cannot override` it
  - The method can no longer be modified
- It prevents the method from being modified while extending to sub-classes
  - It is a method that cannot be redefined in child classes, preventing child classes from changing the behavior of the parent class's method
  - This helps maintain program consistency and prevent bugs!

<br>

### Final Variable

- It becomes a `constant value` that does not change and cannot be reassigned
- Since it cannot be modified, an initial value is mandatory
  - However, if it is a variable inside an object, initialization through a `constructor` or `static block` is allowed
- The scope of the unmodifiable value is limited to the `value of that variable`
  - That is, when referencing another object, the internal values of the referenced object can be changed
- `public static final`
  - It is a class constant that does not require an instance
  - It can be used once the class is loaded into memory
    - It is used in the form of `class.constant`
  - Likewise, it must be initialized at the time of declaration
