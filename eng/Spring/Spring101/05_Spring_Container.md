# Spring Container

> The core of Spring!
>
> Manages Beans (objects) that constitute a program using DI (Dependency Injection)
>

## Types

### BeanFactory
>
> Loads Beans when they are used (Lazy-loading)

- A class that creates and manages Bean objects
- Responsible for `managing Beans`, including creating, looking up, and returning Beans
- BeanFactory loads Bean definitions immediately, but does not instantiate the Bean itself until it is called
  - When `getBean()` is called, only then does the Factory instantiate the received Bean using Dependency Injection (DI) and set the Bean's properties → `On-demand` approach
- Focuses on the basic IoC functionality of creating Beans and configuring relationships
- `How Beans are created and loaded`
  - `BeanFactory` uses `Lazy-loading`
  - Instances are created and loaded at the point when a method or class receives a Bean loading request
    - Therefore, instances are created and loaded at the point when requested by the `.getBean()` method

<br/>

### ApplicationContext
>
> Loads all Beans at runtime startup (Pre-loading)

- Similar to BeanFactory, but a more enhanced form of container
- Focuses on overseeing the overall control of Bean creation, relationship configuration, etc., by referencing separate information
- `How Beans are created and loaded`
  - `ApplicationContext` uses `Pre-loading`
  - All Beans and configuration files are instantiated and loaded when a load request is made by the ApplicationContext

<br/>

### BeanFactory vs ApplicationContext

- The reason they are divided into two approaches is because of the relationship between `usage frequency` and `resources used`
  - If a Bean is not frequently used, it should be loaded only when actually requested to save consumed resources (Lazy-loading) → `Use BeanFactory`
  - If a Bean is frequently used, it is better to load it all at once (Pre-loading) → `Use ApplicationContext`
