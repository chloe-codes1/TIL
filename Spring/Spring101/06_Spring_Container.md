# Spring Container

> 스프링의 핵심!
>
> DI (의존성 주입)를 사용하여 프로그램을 구성하는 Bean (객체)를 관리한다
>

## 유형

### BeanFactory
>
> Bean을 사용할 때 로딩 (Lazy-loading)

- Bean 객체를 생성하고 관리하는 class
- Bean을 생성하고, 조회하고 돌려주는 등 `Bean을 관리`하는 기능을 담당한다
- Bean Factory는 Bean의 정의를 즉시 로딩하지만, Bean 자체를 호출할 때 까지는 인스턴스화 하지 않는다
  - `getBean()` 이 호출되면, 그  때서야 Factory가 의존성 주입 (DI)를 사용하여 받은 Bean을 인스턴스화 하고, Bean의 특성을 설정한다 → `On-demand` 방식
- Bean을 생성하고, 관계를 설정하는 IoC의 기본 기능에 초점이 맞춰져 있다
- `Bean을 생성하고 로딩하는 방식`
  - `BeanFactory` 는  `Lazy-loading` 을 한다
  - Method나 class가 Bean loading 요청을 받는 시점에 인스턴스를 만들고 로딩하는 방식이다
    - 그래서 `.getBean()` method에 의해 요청을 받는 시점에 인스턴스를 만들고 로드된다

<br/>

### ApplicationContext
>
> 런타임 실행 시 모든 Bean을 로딩 (Pre-loading)

- BeanFactory와 유사하지만, 더 향상된 형태의 컨테이너다
- 별도의 정보를 참고해서 Bean의 생성, 관계 설정 등의 제어를 총괄하는 것에 초점을 맞추고 있다
- `Bean을 생성하고 로딩하는 방식`
  - `ApplicationContext` 는 `Pre-loading` 을 한다
  - 모든 Bean들과 설정 파일들이 ApplicationContext에 의해 로드 요청이 될 때 인스턴스로 만들어지고, 로드된다

<br/>

### BeanFactory 와 ApplicationContext

- 두 가지 방식으로 나누어진 이유는 `사용 빈도`와 `사용되는 자원의 관계` 때문이다
  - 자주 사용되지 않는 Bean이라면 소모되는 자원을 아끼기 위해 실제 요청 시에만 로딩하고 (Lazy-loading) → `BeanFactory 사용`
  - 자주 사용되는 Bean이라면 한 번에 로드하는 것 (Pre-loading)이 좋다 → `ApplicationContext 사용`
