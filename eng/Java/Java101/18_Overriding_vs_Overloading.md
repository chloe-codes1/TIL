# Overriding vs Overloading

<br>

## Overloading

### What is Overloading?

Even if a method with the same name already exists in a class, if the `number or type of parameters` is different,

you can define a method using the same name -> defining a new method

<br>

### Conditions for Overloading

- Method `names must be the same`, and the `number` or `type` of `parameters` must be different
- Having only a different return value does not allow overloading!

<br>

### Reasons for Using Overloading

- Methods with the same functionality can be used under a single name
  - ex) println
    - Even when various types of parameters such as int, double, boolean, String are passed as arguments, we don't know how those functions are executed internally, but we can see that they print output to the console
- Method names can be conserved

<br>

## Overriding

### What is Overriding?

- `Redefining` a method inherited from a parent class in a child class
- While the inherited method could be used as is, overriding becomes necessary when the child class needs to modify it to fit the situation

<br>

### Conditions for Overriding

- Since overriding means redefining only the behavior of a method, the method's `declaration must be exactly the same as the original method` (method name, parameters)
  - However, the return type of the method can be changed if it is a type that can be type-converted to the parent class's return type
- The `access modifier` cannot be changed to a `narrower scope` than the parent class's method
- A `broader range` of `exceptions` cannot be declared than the parent class's method

<br>

### Purpose of @Override

- The @Override annotation serves the function of `verifying overriding`
- If overriding has not actually been implemented, it outputs a `compile-time error`
