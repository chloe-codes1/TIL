# Inheritance in Java

<br>

## Inheritance

- Uses the Extends keyword
- Java uses Single Inheritance
  - Only one class can be inherited at a time

- ex) Dog extends Animal

  => The Dog class inherits from the Animal Class

- The parent class can be accessed with the super keyword

  => super();

- The implicitly called super() invokes the parent's default constructor

- The parent constructor of all objects is Object!!!!!!!!

- When loaded into memory, the parent is on top and the child is on the bottom

- When searching for data, it goes from the bottom child upward to the parent

  => It searches from the bottom and goes up if not found

- ex) If the data type is Dog, both Animal and Object are accessible

- Using super, you can skip one child class and search from the parent

- is-a relationship

  => The data type of all objects can be the parent

  - Data compatibility is only possible in parent-child relationships
    - Not possible in sibling relationships!
  - A parent type cannot access child data at the bottom

<br>

### `super();`

- Calls the parent's constructor.
  - Even if removed, it is automatically included!
  - Even if absent, it is automatically called!

- If not visible, it is omitted!
- Like the this() method, it is only allowed in the first statement!
  - So you can tell that super() is absent in constructors where the this() method is used
  - super.______ allows searching from the parent area instead of the child!
- Both `this. keyword` and `super. keyword` can only be used in the **heap area**!!!!

<br>

![img](https://lh5.googleusercontent.com/6Tv949yM4OxWABprfuItlzqQYXbhSzxR-EYGptVGBXO-39xikX6xOlJbM_9ZcJLff61_Y8rOeWoF4hb_YW3dwqvvPpKCJcm06_T6Hq-LHINf_uJ_cw7oo9LJX8yxgH1-20iJNeGc)

<br>

<br>

## Method Overloading

- Multiple methods with the same name can exist within a single class
  - However, the type or number of the method's parameters must be different!

<br>

<br>

## Constructor

- A function created when an object is created

- The constructor function name is the same as the class name
- Return type must not be mentioned - method overloading applies
- Constructors can also be called by method name
  - this();
- A constructor with no parameters = default constructor
- public can be added or omitted
- Access modifiers can be specified

<br>

<br>

## Overriding in Java

> In any object-oriented programming language, Overriding is a feature that allows a subclass or child class to provide a specific implementation of a method that is already provided by one of its super-classes or parent classes. When a method in a subclass has the same name, same parameters or signature and same return type(or sub-type) as a method in its super-class, then the method in the subclass is said to *override* the method in the super-class.

<br>

- Redefining a function inherited from the parent!
- Just bring over the method declaration as is!
- Overriding is not mandatory!
  - So no error is shown.. fix it yourself~
  - <br>

![overriding in java](https://lh6.googleusercontent.com/i42VjCn-_E1fOx1xyW73cCB6vZI5ClO3yBporRbLONAslhZMBz9BBWCBysDcR2vgkoW5VdHsclYkzUo1-_6ig4FrlO1fbfGT5R0v3714e340RmjkyOZchdZqOkDp-_U4Rz_l9eLB)

<br>

**![img](https://lh6.googleusercontent.com/cATWBSmNqpRxlCjGU_ixiGLNwIvBbha-_mb0WW-9m6PUIKYs5mfdqUsuZlH8uJKaIrBjBNpd6e7FKAu3W8cGAjXooOW73DwWYVN67WxXe-do0aoKrVCpkXIxixRSeiYkjM9WvSM6)**

- If inheritance is not mentioned, it can be seen that java.lang.Object is automatically inherited!
- Class Animal extends **Object**!
- `Object` = methods available to all objects
  - At the very top of any object is Object!

<br>

### Is a

- The data type of all objects can be the parent!!
  - The data type of all objects is Object!
    - why? Because Object is at the very top of all objects' memory!

<br>

ex1)

```java
Animal a = new Animal();
Object
```

- Since the parent object of Animal is Object, Object can also be used as the data type when declaring an object!
- However, if the type is Object, the data inside Animal cannot be accessed, and the accessible type is limited to the very top!

<br>

 ex2)

```java
Animal d = new Dog();
Dog
    Object
```

- Since Dog has Animal as a parent object, Animal or Object can be used when declaring an object!
  - When declared as Animal, Dog is not accessible; Animal and above (Animal + Object) are accessible

- All objects in Java can be of Object type, but the accessible information is limited!

- The parent object can be accessed through type casting!

  => Casting in objects -> Up casting

  Ex) ((Animal)d).kind;

  ​ => If you up-cast Dog, which is originally Dog, to Animal, you can directly access Animal

<br>

![img](https://lh4.googleusercontent.com/VmrL993swpj5LtVtY29bTA1VVKoKnle6KNYuGfUUTtjlpxIUSWVUyevCkv5u53F2C9TzuD35JKflEneZKjjBdFlXtHVLUoT-lHJNBOLmgp6f08vxjCfT9SoMYN53Jr-clXQFqMlZ) <br><br>
![img](https://lh4.googleusercontent.com/khSU0qSc8P28hUS4iJogUIISKPCj7niL8JNQDzkOcbJG9omJj-jvBKvKUfjfSNQCK8A982-KFHxTO9dxJWRoQJlBknWSBTlFwr73o73mt0_0xAjEHdzBXXQ3sI4YiKAIVN7Nk2Q2) <br>

<br>

### Annotations

: a tag that represents the metadata i.e. attached with class, interface, methods or fields to indicate some additional information which can be used by java compiler and JVM.

-> ex) `@Override`

<br>

### Polymorphism

- the ability of an object to take on many forms
  - By incorporating overriding techniques, a single method can accept various types of objects!

<br>
