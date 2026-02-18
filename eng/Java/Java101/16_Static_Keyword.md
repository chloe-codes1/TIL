# Static Keyword
>
> The static keyword can be applied to fields, methods, and classes
>

<br>

### Static Field (Variables, Constants)

- When you declare a variable inside a class, it is declared as a member variable and must be accessed through an object like [`car.name`](http://car.name)
- However, if you declare a variable using the static keyword, it can also be `accessed through the Class`
  - When accessed through the Class, it can be `accessed externally` `without creating an object`
  - It can also be accessed through an object, but accessing through the Class is recommended
    - Why?
      - Because it is difficult to distinguish whether you are accessing a member variable or a static variable!
- Variables declared as static are created and initialized `when the program is executed`
  - Therefore, even without creating an object, the `variable is already in a created state`!
- Declaring as `final static` makes it a `constant` whose value cannot be changed
  - Conventionally, to easily distinguish static constants, names are written using only `uppercase letters` and underscores (`_`)
- `Access modifiers`
  - When declaring a static field, you can set the scope you want to expose using access modifiers
- `Reasons for use`
  - Most static fields are used when `declaring constants`
    - When you declare a constant with the `final static` keyword, other classes can also access the constant
    - It can also be declared as a member variable, but implementing it this way means each object holds the constants, which can increase the object's size
  - Declaring too many variables as static moves away from object-orientation and can easily lead to spaghetti code (complex tangled code)

<br>

### Static Method

- Static methods are similar to static fields
  - If you use the static keyword when declaring a method, you can call that method without creating an object
- Since it is difficult to distinguish whether you are calling an object method or a static method, it should `only be called through the Class`
- `Cautions`
  - A static method can be called without creating an object, which means `the method is separated from the object`
    - Therefore, keywords like `super` and `this` cannot be used `inside the method`,
    - and it also `cannot access` the class's `member variables`
  - In static methods, only variables declared inside the method, static fields, and static methods can be accessed
- `Reasons for use`
  - Static methods are typically used to create `Utils` and `Helper` classes
    - ex) Creating a Math Utils class

      ```java
      public class Math {
          public static double sqrt(double num) {
              // ....
          }

          public static double sum(double num1, double num2) {
              // ....
          }
      }
      ```

      - It has the advantage of grouping math-related methods under a class called Math (`grouping`)

<br>

### Static Class

- Declaring a class using the static keyword separates it from the upper class
  - An `Inner class` is `connected to the upper class`, so it can access the upper class's member variables
    - Declaring a sub-class as static makes it impossible to access the upper class's member variables!
    - A `sub-class declared as static` is called a `static nested class`
  - A `Static nested class` can have objects created directly from the outside even without the upper class being created

    ```java
    Car.Wheel wheel = new Car.Wheel();
    ```

    -> This is the biggest difference between `Inner class` and `Static nested class`

- `Cautions`
  - Static class is only possible `when declaring a sub-class`
    - Trying to declare the upper class as static will cause a compile error
- Reasons for using `static class`
  - The benefit of creating an Inner class as a static class is `grouping`
    - There is an advantage of being able to group related classes by declaring classes associated with a certain class below it
      - This can also be done with Inner classes, but Inner classes are `connected` to the upper class and are not independent classes!

<br>

### Summary of Static Keyword Advantages

- The common aspect of the static keyword is `separation from objects`
  - It allows access without creating an object!
- It has the advantage of `Grouping`
  - Methods and classes related to a certain class can be declared as static below it to gather them in one place!!
