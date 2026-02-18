# == Operator, equals(), hashCode

> equals and hashCode are defined in the Object class, which is the parent object of all Java objects
>
> -> Therefore, all Java objects inherit the equals and hashCode functions defined in the Object class

<br>

### == Operator

- When the operands are `primitive types` (int, byte, short, long, float, double, boolean, char), it `compares values`,
- When the operands are other `reference types`, it `compares the addresses they point to`

<br>

### equals()

```java
public boolean equals(Object obj) {
    return (this == obj);
}
```

- Used to check whether 2 objects are identical
- It checks whether the 2 objects refer to the same thing
  - That is, 2 objects are identical only when they point to the `same memory address`
- When we create 2 identical strings, the 2 strings are allocated in different memory locations
  - However, the reason equals returns true is that the String class `overrides` the equals method to return true when the string contents are the same
    - It compares each character one by one and returns true if they are all identical
    - Therefore, even different objects are judged to be identical if they have the same string

<br>

### hashCode()

```java
public native int hashCode();
```

- It refers to a unique integer value that can identify an object
  - In the Object class, it is set to return the `memory address of the object stored in heap memory`
- The `native` keyword means the method is implemented using native code called `JNI (Java Native Interface)`
  - native is a keyword applicable only to methods, used when utilizing parts implemented in languages other than Java through JNI in Java
    - It is a keyword that enables using other languages from Java!
- hashCode is `used to determine the location where data is stored` when using data structures such as `HashTable`
