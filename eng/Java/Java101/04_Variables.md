# Variables in Java

<br>

### 1. Member variable (Instance variable)

> Declared in a class, but outside a method

```
Class A {

 String name;

}
```

- A member of the `Class`

- A variable declared inside a Class

- Created when an `Instance` is created

- To read or store the value of an instance variable, an Instance must be created first!

- If an initial value is not set, automatic default initialization occurs

  ex) No need to write String name = null;



<br>

### 2. Local variable

```
Public Static Void main(~~~) {

	String name;

}
```

- A member of a function

- A variable declared inside a method (function)

  - Can only be used within the method

- Receives memory allocation when the method is executed, and is destroyed when it ends, becoming unusable

- Default initialization does not occur

  ex) You must write String name = null;

<br>

### 3. Class variable (Static variable)

> Declared with the `static keyword` in a class, but outside a method, constructor, or block

- Just add `static` to an instance variable
- While instance variables have unique values for each instance, class variables share a common value among all instances
  - When all instances of a class need to have a common value, declare it as a class variable!
- Created when the class is loaded (= **loaded into memory only once**) and maintained until the program terminates
- Adding `public` makes it a **global variable** accessible from anywhere within the same program
- Unlike instance variable access, class variables are accessed through the class name & class variable name without creating an instance



<br><br>

### Reasons for `Null Assign` (from docs.oracle)

: **Assign null to Variables That Are No Longer Needed**

Explicitly assigning a null value to variables that are no longer needed helps the garbage collector to identify the parts of memory that can be safely reclaimed. Although Java provides memory management, it does not prevent memory leaks or using excessive amounts of memory.

An application may induce memory leaks by not releasing object references. Doing so prevents the Java garbage collector from reclaiming those objects, and results in increasing amounts of memory being used. Explicitly nullifying references to variables after their use allows the garbage collector to reclaim memory.

One way to detect memory leaks is to employ profiling tools and take memory snapshots after each transaction. A leak-free application in steady state will show a steady active heap memory after garbage collections.

<br>

<br>

*Resources that are no longer needed must be null-assigned!*

-> If you don't null-assign, the resources consume too much memory, resulting in poor performance!

<br>

 But, null-assigning doesn't release all resources

```
input.close();

Input = null;
```

  -> You need to do this to release all resources
