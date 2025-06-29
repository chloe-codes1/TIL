# Register a Spring Bean in the Spring IoC container

<br/>

### Java Annotation을 사용하는 방법

> @Component 사용하기

- 자바 소스코드에 추가하여 사용할 수 있는 메타데이터의 일종인 annotation 중 `@Component` annotation을 사용하여 `IoC Container`에 `Spring Bean`을 등록할 수 있다
  - 개발자가 직접 개발한 class를 Bean으로 등록하고자 하는 경우 `@Component` annotation을 활용한다!
- `@Component` annotation이 등록되어 있는 경우에 Spring이 annotation을 확인하고, 자체적으로 Bean으로 등록한다
  - ex)
    - Controller를 등록할 때 사용하는 `@Controller` annotation에는 아래와 같이  `@Component` annotation이 있는 것을 확인할 수 있다

      ```java
      // Controller.java
      @Target({ElementType.TYPE})
      @Retention(RetentionPolicy.RUNTIME)
      @Documented
      @Component
      public @interface Controller {
      
        /**
        * The value may indicate a suggestion for a logical component name,
        * to be turned into a Spring bean in case of an autodetected component.
        * @return the suggested component name, if any (or empty String otherwise)
        */
        @AliasFor(annotation = Component.class)
        String value() default "";
      
      }
      ```

- `@Component` 를 이용하면, Main 또는 App class에서 `@ComponentScan` 으로 컴포넌트를 찾는 탐색 범위를 지정해 주어야 한다
  - but, SpringBoot를 사용한다면 `@SpringBootConfiguration` 하위에 기본적으로 포함되어 있어 별도의 설정이 필요 없다

<br/>

### Bean Configuration File에 직접 Bean을 등록하고, ApplicationContext를 이용해서 Bean을 가져오는 방법

> @Bean & @Configuration 사용하기

- `@Configuration` 과 `@Bean` annotation을 이용하여 Bean을 등록한다
  - 아래와 같이 `@Configuration` 을 이용하면 Spring Project에서의 Configuration 역할을 하는 Class를 만들고, Bean을 설정할 수 있다

    ```java
    import org.springframework.context.annotation.Configuration;
    
    // 1개 이상의 Bean을 등록하고 있음을 명시하는 어노테이션 
    @Configuration
    public class ApplicationConf {
        @Bean
        public Person person(){  // 메소드 이름이 bean의 id
            return new Person();
        }
    
        @Bean
        public Body body(){
            return new Body();
        }
    }
    ```

  - `@Bean` 을 사용하는 class 에는 반드시 `@Configuration` annotation을 활용하여 해당 class에서 Bean을 등록하고자 함을 명시해주어야 한다
    - `@Configuration` annotation 없이 `@Bean` annotation 만 사용해도 Spring Bean으로 등록은 되지만, method 호출을 통해 객체를 생성할 때 `싱글톤` 을 보장하지 못한다
  - 참고로, Bean의 설정을 담당하는 `@Configuration` annotation도 내부적으로 `@Component` annotation을 가지고 있어, `@Configuration` 이 붙은 class도 Spring Bean으로 등록된다
- `@Bean` & `@Configuration` 으로 생성한 Bean 사용하기
  - `ApplicationContext` 를 만들고, `.getBean()` method로 Bean을 가져와 사용한다

    ```java
    public class Application {
        public static void main(String[] args){
            AnnotationConfigApplicationContext context =
                new AnnotationConfigApplicationContext(ApplicationConf.class);
                
            Person person = (Person)context.getBean(Person.class);
            person.say(); // print : "hi"
        }
    }
    ```
