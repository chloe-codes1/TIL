# Register a Spring Bean in the Spring IoC Container

<br/>

### Using Java Annotations

> Using @Component

- Among annotations, which are a type of metadata that can be added to Java source code, the `@Component` annotation can be used to register a `Spring Bean` in the `IoC Container`
  - Use the `@Component` annotation when you want to register a class that you developed directly as a Bean!
- When the `@Component` annotation is registered, Spring recognizes the annotation and automatically registers it as a Bean
  - ex)
    - In the `@Controller` annotation used to register a Controller, you can see that the `@Component` annotation is present as shown below

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

- When using `@Component`, you must specify the scanning range for components with `@ComponentScan` in the Main or App class
  - However, if using SpringBoot, it is included by default under `@SpringBootConfiguration`, so no separate configuration is needed

<br/>

### Registering Beans Directly in a Bean Configuration File and Retrieving Beans Using ApplicationContext

> Using @Bean & @Configuration

- Beans are registered using the `@Configuration` and `@Bean` annotations
  - As shown below, using `@Configuration` creates a Class that serves as Configuration for the Spring Project, where Beans can be configured

    ```java
    import org.springframework.context.annotation.Configuration;

    // Annotation indicating that one or more Beans are being registered
    @Configuration
    public class ApplicationConf {
        @Bean
        public Person person(){  // The method name becomes the bean's id
            return new Person();
        }

        @Bean
        public Body body(){
            return new Body();
        }
    }
    ```

  - In a class using `@Bean`, you must use the `@Configuration` annotation to indicate that the class intends to register Beans
    - Using only the `@Bean` annotation without the `@Configuration` annotation will still register as a Spring Bean, but `singleton` behavior is not guaranteed when creating objects through method calls
  - Note that the `@Configuration` annotation, which is responsible for Bean configuration, also internally has a `@Component` annotation, so the class with `@Configuration` is also registered as a Spring Bean
- Using Beans created with `@Bean` & `@Configuration`
  - Create an `ApplicationContext` and use the `.getBean()` method to retrieve and use Beans

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
