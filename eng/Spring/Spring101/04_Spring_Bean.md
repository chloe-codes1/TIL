# Spring Bean

<br/>

### What is a Spring Bean?

> Java objects managed by the Spring IoC container are called Beans
>
> → POJOs (Plain Old Java Objects) managed by the Spring DI Container

- In Java programming, you would create a Class and use the new keyword to directly create and use the desired object,
  - In Spring, instead of objects directly created with new, `Java objects managed by Spring` are used
  - These `Java objects created and managed by Spring` are called `Beans`
- In Spring Framework, methods like `ApplicationContext.getBean()` are used to obtain `Spring Beans` -- getting Java objects directly from Spring

<br/>

### Characteristics of Spring Bean

- As POJOs (Plain Old Java Objects), they are the core objects that constitute a Spring application
- They are created and managed by the Spring IoC container (or DI container)
- In Spring, Beans are created in `Singleton` mode by default

<br/>

### Components of a Spring Bean

- `class`
  - The Java class to register as a Bean
- `id`
  - The unique identifier of the Bean
- `scope`
  - The method for creating the Bean
    - singleton, prototype, etc.
- `constructor-arg`
  - Parameters to pass to the constructor when creating the Bean
- `property`
  - Arguments to pass to the setter when creating the Bean

<br/>

### Spring Bean Scope

#### What is Spring Bean Scope?

> The range managed by a Bean is called Bean Scope
>
- By default, Beans are created with `Singleton scope`
- This is to create only `one` instance of a specific type of Bean and `share` it for use,
  - Because of this, writing code that stores state in a Bean (`Stateful` code) can cause `concurrency issues`
- Depending on requirements and the functionality being implemented, there may be cases where a non-singleton is needed, and the `scope` keyword is provided to explicitly distinguish this

#### Types of Scope

- `singleton` scope
  - The default scope in the Spring framework
  - Maintained as `one object` from the start to the end of the Spring container
- `prototype` scope
    > Declared with `@Scope("prototype")`
  - A scope where the Spring container is only involved in the `creation and dependency injection` of the Prototype Bean, and no longer manages it
  - Unlike singleton, prototype scope only handles `up to dependency injection`, so returning the Bean must be done by the client directly
  - When a request comes in, a `new instance is always created and returned`, and it is not managed afterward
  - When a Bean is registered as Prototype, a different instance is returned each time `.getBean()` is called
  - Since it only injects dependencies and then releases, `@preDestroy` is not observed
    - When the container is terminated with the `close()` method, the `@preDestroy` method is not called
  - `Order`
      1. The client requests a Bean.
      2. The Spring DI container creates a new Bean for the request.
      3. Dependency Injection (DI) is performed on the newly created Bean.
      4. Initialization tasks such as @PostConstruct are performed.
      5. This created Bean is not managed by the Spring container and is returned to the client.

      → What we can learn from this is that different clients will have beans with different references, and while @PostConstruct will be called, @PreDestroy will not.

- `Problem when singleton scope and prototype scope are mixed`

    > A prototype bean inside a singleton bean is newly created at the time of singleton bean dependency injection, but since that reference keeps being used, it is only newly created once and then maintained along with the singleton object
  - `Method to create a new internal prototype bean each time a singleton bean is requested`
    - `Dependency Lookup` → Finding and using dependencies directly
      - The Spring bean container itself is injected as a dependency, and when a prototype scope bean is needed, the `dependency bean is looked up directly from the container`
      - This method of directly finding and using needed dependencies is called `Dependency Lookup`
      - `Problems`
        - The code itself becomes dependent on the entire Spring Context
        - Unit testing becomes difficult
    - `ObjectProvider`
      - Instead of injecting the prototype scope bean as a dependency, an ObjectProvider with the prototype scope bean as its type is injected as a dependency bean, as shown below

          ```java
          private ObjectProvider<PrototypeBean> prototypeBean;
          ```

      - When a prototype scope bean is needed, a new prototype scope bean can be created and retrieved through the `getObject()` method

- `web scope`

    > A scope that operates only in a web environment
    >
    > Spring manages Beans set to web scope until the termination point of the scope
    >
    > Termination methods are called (both @PreDestroy and @PostConstruct are available)
  - `request`  → @Scope(value = "request")
    - A scope maintained from when an HTTP request comes in until it goes out
    - A separate bean instance is created and managed for each HTTP request
    - Web scope request creates a separate Bean each time many users send requests
  - `session`
    - A scope maintained from when an HTTP Session is created until it is terminated
  - `application`
    - A scope with the same lifecycle as `ServletContext`
  - `websocket`
    - A scope with the same lifecycle as `Websocket`

### Spring Bean Lifecycle

#### Bean Lifecycle

> The Spring container manages the lifecycle of Bean objects, which have the following lifecycle

1. Spring container creation
2. Bean object creation
3. Dependency configuration
4. Initialization (callback)
5. Bean usage
6. Bean destruction (pre-destruction callback)
7. Spring container termination

> The lifecycle order of Beans managed by the Spring container
>
>
> → `Object creation - Dependency configuration - Initialization - Destruction`

- When the Spring container is `initialized`, it creates Bean objects according to configuration information and configures `dependencies`
- When dependency configuration is complete, the Bean object calls the designated method for `initialization`
- When the container is terminated, the Bean object calls the designated method to process the Bean object's `destruction`

#### Bean Lifecycle Callback

- What is a Bean Lifecycle Callback?
  > Spring provides various features to notify the Bean of the `initialization timing` through `callback` methods once `dependency injection` is complete.
  >
  > It also provides a `destruction callback` just `before` the Spring container `terminates`

  - `Initialization callback`
    - Called after the Bean is created and the Bean's dependency injection is complete
  - `Pre-destruction callback`
    - Called just before the Bean is destroyed
    - `singleton` beans are terminated together when the Spring container terminates, so the `pre-destruction callback` occurs just before the Spring container terminates

- Types of callbacks
  - `Interfaces (InitializingBean, DisposableBean)`
    - → Rarely used
  - `Specifying initialization and termination methods in configuration information`
    - Initialization and destruction methods can be specified in bean registration configuration information as follows:

      ```java
      @Bean(initMethod="init", destroyMethod="close")
      ```

    - `Pros`
      - Method `names` can be set freely
      - Beans do not depend on Spring code
      - Since `configuration information` is used instead of code, initialization and termination methods can be applied to `external libraries` whose code cannot be modified
  - `@PostConstruct, @PreDestroy annotation support` → Most commonly used
    - `Pros`
      - The most convenient way to perform initialization and termination.
        - It is the most recommended approach in modern Spring.
        - Simply attaching an annotation makes it very convenient. (No need to implement interfaces and override.)
      - It is not a Spring-specific technology but a `Java standard`.
        - `javax.annotation.PostConstruct`
        - Therefore, it works in other containers besides Spring.
      - Works well with `component scanning`. (Since it's not @Bean configuration!)
    - `Cons`
      - Cannot be applied to external libraries
        - If you need to initialize/terminate external libraries, use the @Bean functionality!
