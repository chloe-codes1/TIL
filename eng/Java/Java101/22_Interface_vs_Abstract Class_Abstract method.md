# Interface vs Abstract Class, Abstract method

<br>

### Interface

- `Description`
  - Used when `common functionality` is needed `without being bound by inheritance relationships` between parent and child.
    - `Abstract Methods` are defined,
    - and the `implementing` classes `Override` each function to implement it in various forms, so it is related to `polymorphism`
  - An Interface exists to `enforce` `the same methods and behavior` on the classes that implement it
- `Advantages`
  - It can compensate for the `limitations of Abstract Classes` caused by Java's inability to support `multiple inheritance`
- `Disadvantages`
  - If all classes use an Interface, there is the `inconvenience of having to Override and redefine` `commonly needed functionality` in all implementing classes
- `Summary`
  - Interfaces are convenient to use when `specifying common functionality` for classes that inherit from different Abstract Classes

<br>

### Abstract method

- `Description`
  - It refers to a method that `must be overridden` in a child class
  - A method is divided into a `declaration part ()` and an `implementation part {}`, and an abstract method is one where only the declaration is written without the implementation
  - Abstract methods are used because the method content varies depending on which class inherits it
  - The `implementation part {}` must be written in the sub-class that inherits the class
    - If the implementation is not written, an `error` occurs!
  - `Comments` should describe what functionality the method performs
  - `abstract` is not written on `overriding` methods

<br>

### Abstract Class

- `Description`
  - A class that has even one `Abstract method` is called an `Abstract class`
    - That is, a regular class cannot have abstract methods!
  - A child class that inherits an Abstract class must `override` the `abstract methods`
    - The abstract class `forces redefinition` of abstract methods on child classes
    - `abstract class` <-> `final class`
      - It is the opposite of a final class which `prohibits inheritance` to restrict overriding!
  - Abstract classes are intended for `program design`
    - On the other hand, regular classes are intended for creating multiple objects and storing data
  - Abstract classes `cannot be created as objects`
    - The child class must inherit the abstract class, `override` the abstract methods to complete the implementation, and then use the child class to create objects
  - In a parent-child relationship, when `inheriting (extends)` the Abstract Class, among `child classes` that inherit the same parent Class (here, the Abstract Class):
    - Each `implements` `common functionality`,
    - `extends` it,
    - and it is related to `inheritance`
      - Inheritance is used to utilize and extend the functionality of the SuperClass!
  - Inheriting Abstract Classes enables `distinction` between classes
- `Advantages`
  - Once `design` is completed in the abstract class, it is convenient to `extend functionality` by inheriting in child classes
  - Since `implementation of abstract methods is enforced` in child classes, the `degree of standardization` is increased
  - Since `common aspects` of classes can be managed in one place, `development and maintenance` become convenient
- `Disadvantages`
  - Since Java does not support `multiple inheritance`, there are limitations in `enforcing` `Abstract Methods` that must be implemented using only `Abstract Classes`
  - What if multiple inheritance were possible?

    ```java
    class Vehicle extends Car, Motorcycle {
        @Override
        public void run(){
            super.drive();
        }
    }
    ```

    - If a drive() method is defined in both Car and Motorcycle, it becomes `ambiguous which one is being inherited and Overridden`
    - This is the `ambiguity of multiple inheritance`, and this is why Java has blocked multiple inheritance

<br>

### Abstract Class vs Interface

- Abstract Class represents `IS - A "is a"`,
  - while Interface represents `HAS - A "is capable of"`
- Abstract Class is about `inheritance`,
  - while Interface is about `polymorphism`
