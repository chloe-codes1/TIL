# IoC: Inversion of Control

> “Don’t call me, I’ll call you”
>
> 개발자가 아닌 툴이 제어권을 가져 클래스가 의존 객체를 직접 만드는 것들이 아니라 주입받아서 사용하는 것
>
> → 코드의 흐름을 제어하는 주체가 바뀌는 것
<br/>

- IoC가 적용된 경우, 객체의 생성을 `특별한 관리 위임 주체` 에게 맡긴다
  - 이 경우 사용자는 객체를 직접 생성하지 않고, 객체의 생명주기를 컨트롤하는 주체는 다른 주체가 된다
  - 즉, `사용자의 제어권을 다른 주체에게 넘기는 것` 을 제어의 역전, Inversion of Control 이라고 한다
- `ApplicationContext`와 `BeanFactory`(ApplicationContext는 BeanFactory를 상속받는다) 인터페이스 덕분에 `Bean으로 지정한 모든 클래스를 인스턴스로 등록`해주어 다른 클래스에서 의존관계가 필요하다면 이 Bean(스프링 IoC 컨테이너가 관리 하는 객체)으로 등록된 인스턴스들을 전달해주어 의존성 주입(Dependency Injection)이 가능해진다.
