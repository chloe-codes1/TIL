# Annotation

<br>

## Characteristics of Annotations

- Annotation originally means comment, and it is a syntax based on interfaces
  - Although its role differs from comments, like comments, it can be attached to code to give classes special meaning or inject functionality
- Using annotations, you can directly specify `validation conditions` for data using annotations, making it easy to understand the validation conditions and keeping the code clean
- Annotations are broadly used for `documentation`, `compiler checking`, and `code analysis`
  - The documentation aspect is not widely used because `JavaDoc` exists
  - The essential purpose of annotations is to express metadata in source code
- The timing of interpretation can also be specified (`Retention Policy`)

<br>

## Types of Annotations
>
> There are broadly three types of annotations
>

### 1. `Built-in annotations` built into the JDK

- Mainly for the compiler, providing useful information to the compiler
- ex)
  - `@Override`

    > The `@Override` annotation that appears when overriding a method through inheritance
    >
    - Can only be placed before a method, and it indicates to the compiler that the current method is a method that overrides a super class method
    - Typos can occur in method names when overriding, and from the compiler's perspective, it cannot tell whether a new method is being created or overriding is being done
      - In such cases, the annotation can catch parts where typos may occur
  - **`@Deprecated`**
    - Indicates a method that should no longer be used because it may not be supported in future versions.
  - **`@SupressWarning`**
    - Conveys the programmer's intent to the compiler to remove warnings
  - **`@FunctionalInterface`**
    - Informs the compiler that the following interface is a functional interface
    - Used to prevent mistakes in advance for the same reason as the override annotation

<br>

### 2. `Meta annotations` that are annotations for representing information about annotations

- Annotations used on annotations that determine the behavior target of the annotation
  - Mainly used when defining new annotations
- ex)
  - `@Target`
    - Used to specify the targets to which the annotation can be applied
    - When specifying multiple values, braces { } must be used like in arrays
  - `@Retention`
    - An annotation mainly used when creating custom annotations, which allows you to set how long the annotation's memory should be retained
      - It is about **setting the annotation's `life cycle`**, i.e., determining how long the annotation will live!
    - `Properties`
      - `RetentionPolicy`
        - What is Retention Policy?
          - A policy that defines the lifecycle of an annotation
            - It is used to specify whether annotation information should be retained in the compiled class file
        - Types of Retention Policy
          - `RetentionPolicy.SOURCE`
            - Remains until the source code (.java)
              - Annotation information disappears during the compilation process
            - Mainly used to generate compiler warnings or error messages
          - `RetentionPolicy.CLASS`
            - Remains until the class file (.class) (=bytecode)
              - Not retained at runtime
            - Mainly used for code generation at compile time or for compiler processing
          - `RetentionPolicy.RUNTIME`
            - Remains until runtime (=effectively never disappears)
            - Mainly used to read or modify annotation information through `reflection` at runtime
              - ex) Providing functionality to change or add class behavior at runtime using specific annotations
  - `@Inherited`
    - An annotation that allows the annotation to be inherited by child classes
    - If this annotation is placed on a parent class, the child class is recognized as if it also has this annotation
  - `@Native`
    - An annotation placed on constant fields referenced by native methods
      - A native method refers to a method of the OS where the JVM is installed
      - Native methods are usually written in C, and in Java, only the method declaration is defined without implementation
      - Most methods of the Object class are native methods
      - We have been calling OS methods through the Java language
      - The process of connecting native methods with methods defined in Java is called `JNI (Java Native Interface)`

<br>

### 3. `Custom Annotations` created directly by developers
