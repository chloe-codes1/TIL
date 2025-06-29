# Spring Bean

<br/>

### Spring Bean이란?

> Spring IoC 컨테이너가 관리하는 자바 객체를 빈(Bean)이라고 한다
>
> → Spring DI Container에 의해 관리되는 POJO (Plain Old Java Object)

- Java 프로그래밍에서는 Class를 생성하고 new keyword를 이용하여 원하는 객체를 직접 생성한 후에 사용했던 것을,
  - Spring에서는 직접 new를 이용하여 생성한 객체가 아니라, `Spring에서 관리되는 자바 객체` 를 사용한다
  - 이렇게 `Spring에 의하여 생성되고 관리되는 자바 객체`를 `Bean` 이라고 한다
- Spring Framework에서는 `Spring Bean` 을 얻기 위하여 `ApplicationContext.getBean()` 와 같은 method를 사용하여 Spring에서 직접 자바 객체를 얻어서 사용한다

<br/>

### Spring Bean의 특징

- POJO (Plain Old Java Object) 로써, Spring application을 구성하는 핵심 객체이다
- Spring IoC 컨테이너 (or DI 컨테이너)에 의해 생성되고 관리된다
- Spring에서는 기본적으로 `Singleton` 방식으로 Bean이 생성된다

<br/>

### Spring Bean의 구성 요소

- `class`
  - Bean으로 등록할 Java class
- `id`
  - Bean의 고유 식별자
- `scope`
  - Bean을 생성하기 위한 방법
    - singleton, prototype 등
- `constructor-arg`
  - Bean 생성 시 생성자에 전달할 파라미터
- `property`
  - Bean 생성 시 setter에 전달할 인수

<br/>

### Spring Bean Scope

#### Spring Bean Scope란?

> Bean이 관리하는 범위를 Bean Scope라고 한다
>
- Bean은 default로는 `Singleton scope`로 생성된다
- 특정 타입의 Bean을 `하나만` 만들어두고 `공유`해서 사용하기 위해서인데,
  - 이로 인해 Bean에 상태를 저장하는 코드 (`Stateful` 한 코드)를 작성하는 것은 `동시성 문제` 를 유발할 수 있다
- 요구 사항과 구현하려는 기능에 따라 비 싱글톤이 필요한 경우가 있고, 이것을 명시적으로 구분하기 위해서 `scope` 라는 키워드를 제공한다

#### Scope의 종류

- `singleton` scope
  - Spring framework에서 기본이 되는 scope
  - Spring container의 시작부터 종료까지 `1개의 객체`로 유지된다
- `prototype` scope
    > `@Scope("prototype")` 으로 선언한다
  - 스프링 컨테이너는 Prototype Bean의 `생성과 의존 관계 주입까지만 관여`하고, 더이상 관리하지 않는 scope
  - Prototype scope는 singleton과 달리, `의존 관계 주입까지만` 해주기 때문에 Bean을 반환해 주는건 client가 직접 해야한다
  - 요청이 오면 `항상 새로운 인스턴스를 생성하여 반환`하고, 이후에 관리하지 않는다
  - Prototype으로 Bean을 등록하면, `.getBean()` 을 할 때마다 다른 인스턴스를 반환한다
  - 의존 관계까지만 주입하고 보내주기 때문에 `@preDestroy` 를 볼 수 없다
    - `close()` method로 컨테이너를 종료했을 때 `@preDestroy` method가 호출되지 않는다
  - `순서`
      1. 클라이언트가 Bean 을 요청한다.
      2. 스프링 DI 컨테이너는 요청에 대해 새로운 Bean을 생성한다.
      3. 새로 만든 Bean의 의존 관계 주입(DI) 을 한다.
      4. @PostConstruct 와 같은 초기화작업을 진행한다.
      5. 이 생성된 Bean은 스프링 컨테이너에서 관리하지 않고, 클라이언트에 반환한다.

      → 여기서 알 수 있는 점은, 각자 다른 클라이언트는 각자 다른 참조를 가진 빈을 가지게 된다는 것과 @PostConstruct 는 호출 되겠지만 @PreDestroy 는 호출되지 않을것이란 사실이다.

- `singleton scope와 prototype scope가 섞였을 때의 문제점`

    > 싱글톤 빈 안에 있는 프로토타입 빈은 싱글톤 빈 의존 관계 주입 시점에 새로 생기지만, 그 참조가 계속 쓰이기 때문에 새로 생성만 되고 싱글톤 객체와 함께 유지된다는 문제점이 있다
  - `싱글톤 빈을 요청할 때마다 내부의 프로토타입 빈을 새로 생성하는 방법`
    - `Dependency Lockup` → 의존 관계를 직접 찾아서 쓰기
      - 스프링 빈 컨테이너 자체를 의존 관계로 주입 받고, 프로토타입 스코프 빈이 필요할 때 컨테이너에서 `직접 의존 관계 빈을 찾아 쓴다`
      - 이렇게 필요한 의존 관계를 직접 찾아 쓰는 방법을 `Dependency Lockup` 이라고 한다
      - `문제점`
        - 코드 자체가 Spring Context 전체에 종속적이게 된다
        - 단위 테스트가 어려워진다
    - `ObjectProvider`
      - 프로토타입 스코프 빈을 의존을 의존관계에 주입하지 않고, 아래와 같이 프로토타입 스코프 빈을 타입으로 가지는 ObjectProvider를 의존 관계 빈으로 주입한다

          ```java
          private ObjectProvider<PrototypeBean> prototypeBean;
          ```

      - 프로토타입 스코프 빈이 필요할 때 `getObject()` method를 통해 프로토타입 스코프 빈을 새로 생성해 가져올 수 있다

- `web scope`

    > web 환경에서만 동작하는 scope
    >
    > 스프링에서는 web scope로 설정된 Bean들을 해당 scope의 종료 시점까지 관리한다
    >
    > 종료 method가 호출된다 (@PreDestroy, @PostConstruct 둘 다 가능)
  - `request`  → @Scope(value = "request")
    - HTTP 요청이 들어오고 나갈 때까지 유지되는 scope
    - 각각의 HTTP 요청마다 별도의 빈 인스턴스가 생성되고, 관리된다
    - web scope request는 많은 사용자가 요청을 보낼 때마다 각각의 Bean을 생성하도록 하는 것이다
  - `session`
    - HTTP Session이 생성되고 종료될 때 까지 유지되는 scope
  - `application`
    - `ServletContext` 와 동일한 생명주기를 가지는 scope
  - `websocket`
    - `Websocket` 과 동일한 생명 주기를 가지는 scope

### Spring Bean Lifecycle

#### Bean Lifecycle

> 스프링 컨테이너는 Bean 객체의 lifecycle을 관리해 주며, 아래의 생명 주기를 가진다

1. 스프링 컨테이너 생성
2. Bean 객체 생성
3. 의존 설정
4. 초기화 (콜백)
5. 빈 사용
6. 빈 소멸 (소멸 전 콜백)
7. 스프링 컨테이너 종료

> Spring container가 관리하는 Bean의 라이프사이클 순서
>
>
> → `객체 생성 - 의존 설정 - 초기화 - 소멸`

- 스프링 컨테이너가 `초기화` 될 때, Bean 객체를 설정 정보에 따라 생성하고, `의존 관계` 를 설정한다
- 의존 설정이 완료되면, Bean 객체가 지정한 method를 호출해 `초기화` 한다
- 컨테이너가 종료될 시 Bean 객체가 지정한 method를 호출해 Bean 객체의 `소멸` 을 처리한다

#### Bean Lifecycle callback

- Bean Lifecycle callback이란?  
  > 스프링은 `의존관계 주입`이 완료되면, Bean에게 `callback` method를 통해 `초기화 시점` 을 알려주는 다양한 기능을 제공한다.
  >
  > 또한 스프링 컨테이너가 `종료` 되기 `직전`에 `소멸 callback` 을 준다

  - `초기화 콜백`
    - Bean이 생성되고, Bean의 의존 관계 주입이 완료된 후 호출된다
  - `소멸 전 콜백`
    - Bean이 소멸되기 직전에 호출된다
    - `singleton` bean은 스프링 컨테이너가 종료될 때, singleton bean도 같이 종료되기 때문에 스프링 컨테이너가 종료되기 직전에 `소멸 전 콜백` 이 일어난다

- 콜백 종류
  - `인터페이스(InitializingBean, DisposableBean)`
    - → 잘 안쓴다
  - `설정 정보에 초기화 메서드, 종료 메서드 지정`
    - 빈 등록 설정 정보에 아래와 같이 초기화, 소멸 메서드를 지정할 수 있다.

      ```java
      @Bean(initMethod="init", destroyMethod="close")
      ```

    - `장점`
      - method `이름`을 자유롭게 설정 가능
      - Bean이 스프링 코드에 의존하지 않는다
      - 코드가 아니라 `설정 정보` 를 사용하기 때문에 코드를 고칠 수 없는 `외부 라이브러리` 에도 초기화, 종료 method를 적용할 수 있다
  - `@PostConstruct, @PreDestroy 애노테이션 지원` → 제일 많이 사용
    - `장점`
      - 가장 편리하게 초기화와 종료를 실행할 수 있다.
        - 최신 스프링에서 가장 권장하는 방법이다.
        - 애노테이션 하나만 붙이면 되므로 매우 편리하다. (인터페이스 구현하고 오버라이딩 할 필요없다.)
      - 스프링에 종속적인 기술이 아닌 `자바 표준`이다.
        - `javax.annotation.PostConstruct`
        - 따라서 스프링이 아닌 다른 컨테이너에서도 동작한다.
      - `컴포넌트 스캔`과 잘 어울린다. (@Bean 설정이 아니니까!)
    - `단점`
      - 외부 라이브러리에는 적용하지 못한다
        - 외부 라이브러리를 초기화, 종료해야한다면 @Bean의 기능을 이용하자!
