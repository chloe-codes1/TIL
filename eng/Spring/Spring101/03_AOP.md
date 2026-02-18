# AOP (Aspect-Oriented Programming)

> As an aspect-oriented programming paradigm, it extracts common logic so that it can be executed at various points of a method, reducing code and allowing developers to focus on core concerns while excluding common logic.

<br>

### What is AOP?

- A key principle of a good development environment is to `allow developers to focus only on business logic`
  - There are several important principles for this goal, but the most easily conceivable one is `eliminating repetitive code`
  - The Spring Framework provides ways to reduce such repetitive code and focus only on core business logic
- Common concerns shared by most systems, such as security, logging, and transactions, are not business logic but are essential processing. In Spring, these are called `cross-cutting concerns`
  - Spring allows these cross-cutting concerns to be developed separately
  - `AOP` is a programming paradigm that `separates cross-cutting concerns into modules`
- In the AOP technique, `common functionality` is not directly called from `code implementing core logic`
  - AOP is applied when `compiling` the code implementing core logic, when `loading` the compiled class, or when `creating an object` of the loaded class, inserting common functionality into the core logic implementation code
    - Even if common functionality changes, the code implementing core logic does not need to be modified

<br/>

### Advantages of AOP

1. Developers can focus on developing only the core business logic,
2. When applying different concerns to each project, code modifications can be minimized,
3. Maintainability of desired concerns becomes easier with well-structured code

<br/>

### AOP Terminology

-
  - `Target`
    - A module containing core functionality; it becomes the `subject to which additional functionality is applied`
  - `Advice`
    - Defines the `additional functionality` to provide to the target
    - Types of Advice
      - `Around`
        - Defines additional functionality that needs to be processed at both the before and after points when the target method is called
        - Advice that executes before and after the Joinpoint
      - `Before`
        - Defines additional functionality that needs to be processed before the target method executes
        - Advice that executes before the Joinpoint
      - `After Returning`
        - Defines additional functionality that needs to be processed after the target method executes normally
        - Advice that executes after the Joinpoint method call terminates normally
      - `After Throwing`
        - Defines additional functionality that needs to be processed after the target method throws an exception
        - Advice that executes when an exception is thrown
  - `JoinPoint`
    - A location where advice can be `applied`
    - All methods of the interface implemented by the target object become join points
  - `Pointcut`
    - A regular expression that `selects methods` of the `target to which advice is applied`
      - Determines `where to apply` the Advice!
    - Pointcut expressions start with `execution` and primarily use the method of comparing method `signatures`
  - `Weaving`
    - The process of `inserting` additional functionality (`advice`) into the `joinpoint` of a target determined by the Pointcut
    - Weaving is a core processing step that allows AOP to `add` necessary additional functionality (`advice`) without `affecting` the code of the `core functionality (target)`
  - `Aspect`
    - The basic module of AOP
    - `Aspect = Advice + Pointcut`
    - An Aspect exists as a singleton object
    - When applying the AOP concept, additional functionality embedded within core functionality code can be separated into `independent aspects`
      - Separated additional functionality aspects can dynamically participate at necessary locations at runtime
  - `Advisor`
    - Advisor = Advice + Pointcut
    - Advisor is a special term used only in Spring AOP
