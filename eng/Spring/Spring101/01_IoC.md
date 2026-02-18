# IoC: Inversion of Control

> "Don't call me, I'll call you"
>
> Instead of a developer, the tool takes control, so classes do not create dependent objects directly but receive them through injection
>
> → The entity controlling the flow of code changes
<br/>

- When IoC is applied, the creation of objects is delegated to a `special management entity`
  - In this case, the user does not create objects directly, and the entity controlling the object's lifecycle becomes a different entity
  - In other words, `transferring the user's control to another entity` is called Inversion of Control (IoC)
- Thanks to the `ApplicationContext` and `BeanFactory` (ApplicationContext inherits from BeanFactory) interfaces, `all classes designated as Beans are registered as instances`, and if a dependency is needed in another class, these instances registered as Beans (objects managed by the Spring IoC container) are passed to enable Dependency Injection.
